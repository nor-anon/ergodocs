Constant Seggregation

>Ergo supports flexible language [ErgoTree](https://ergoplatform.org/docs/ErgoTree.pdf) of
guarding propositions which protect UTXO boxes. The propositions are stored in the
blockchain according to ErgoTree serialization format, which is designed for compact
storage and fast script execution and transaction validation.

>However, ErgoTree binary format intentionally doesn't include metadata, which may be
necessary for various Ergo applications.

>This standard defines extended serialization format of contract templates, which may be
reused across different protocol implementations, applications and tools on many
execution environments.

There is ErgoTree serialization section in https://ergoplatform.org/docs/ErgoTree.pdf

- Constant-less lambdas part here https://github.com/ScorexFoundation/sigmastate-interpreter/issues/264

Rational
Massive script validation
Consider a transaction tx which have INPUTS collection of boxes to spend. Every input box can have a script protecting it (propostionBytes property). This script should be executed in a context of the current transaction. The simplest transaction have `1` input box. Thus if we want to have a sustained block validation of `1000` transactions per second we need to be able to validate 1000 scripts per second at minimum. Additionally, the block validation time should be as small as possible so that a miner can start solving the PoW puzzle as soon as possible to increase the probability of the successful mining. For every script (of an input box) the following is done in order to validate it (and should be executed as fast as possible):

1. A Context object is created with SELF = box
2. ErgoTree is traversed to build a cost graph - the graph for the cost estimation
3. Cost estimation is computed by evaluating the cost graph with the current context
4. If the cost within the limit, the ErgoTree is evaluated using the context to obtain sigma
proposition (see SigmaProp)
5. Sigma protocol verification procedure is executed

D.2.2 The Potential Script Processing Optimization
Before an ErgoScript contract can be stored in a blockchain it should be first compiled from its
source code into ErgoTree and then serialized into byte array. Because the ErgoTree is purely
functional graph-based IR, the compiler may perform various optimizations for reducing a size of
the tree. This will have an effect of normalization/unification, in which different original scripts
may be compiled into the identical ErgoTrees and as a result the identical serialized bytes.
In many cases two boxes will have the same ErgoTree up to a substitution of constants. For
example all pay-to-public-key scripts have the same ErgoTree template in which only public key
(constant of GroupElement type) is replaced.
Because of normalization, and also because of script template reusability, the number different
scripts templates is much less than the number of actual ErgoTrees in the UTXO boxes. For
example we may have 1000s of different script templates in a blockchain with millions of UTXO
boxes.
The average reusability ratio is 1000 in this case. And even those 1000 different scripts may
have different usage frequency. Having big reusability ratio we can optimize script evaluation by
performing the step 2 from section D.2.1 only once per unique script.
The compiled cost graph can be cached in Map[Array[Byte], Context => Int]. Every ErgoTree template extracted from an input box can be used as the key in this map to obtain the
graph which is ready to execute.
However, there is an obstacle to the optimization by caching, i.e. the constants embedded in
contracts. In many cases it is natural to embed constants in the ErgoTree body with the most
notable scenario is when public keys are embedded. As the result two functionally identical scripts
are serialized to the different byte arrays because they have the different embedded constants.
D.2.3 Templatized ErgoTree
A solution to the problem with embedded constants is simple, we don’t need to embed constants.
Each constant in the body of ErgoTree can be replaced with an indexed placeholder node (see
63
ConstantPlaceholder). Each placeholder have an index of the constant in the constants collection of ErgoTree.
The transformation is part of compilation and is performed ahead of time. Each ErgoTree have
an array of all the constants extracted from its body. Each placeholder refers to the constant by
the constant’s index in the array. The index of the placeholder can be assigned by breadth-first
topological order of the graph traversal during compilation of ErgoScript into ErgoTree. Whatever
method is used, a placeholder should always refer to an existing constant.
Thus the format of serialized ErgoTree with is shown in Figure 11 which contains:
1. The bytes of collection with segregated constants
2. The bytes of script expression with placeholders
The collection of constants contains the serialized constant data (using ConstantSerializer)
one after another. The script expression is a serialized Value with placeholders.
Using such script format we can use the script expression bytes as a key in the cache. The
observation is that after the constants are segregated, what remains is the template. Thus, instead
of applying steps 1-2 from section D.2.1 to constant-full scripts we can apply them to constant-less
templates. Before applying the steps 3 - 5 we need to bind placeholders with actual values taken
from the constants collection and then evaluate both cost graph and ErgoTree.

[EIP5 is based on this ErgoTree feature](https://github.com/ergoplatform/eips/blob/master/eip-0005.md)

