#Neural Turing Machine
##Introduction and Overall Architecture
<p>
Neural Turing Machines (NTM) can be basically viewed as a machine with simple regular computer architecture, which consists of a controller, memory, and read/write heads, shown as below. The controller, which is made out of neural network (LSTM and feedforward network), makes decisions, takes actions and outputs depending on external input and information read from memory. Meanwhile, parameters of read/write heads and contents stored in memory are updated according to controller decisions.
</p>
<p align="center">
  <img src="img/neuralturing.png">
</p>
<p>
Ideally, NTM can accomplish whatever tasks a general computer is capable of. The main difference between NTM and computers is mechanism set up for controller decisions and actions. In computer, controller (CPU) is designed manually by engineers. Instruction set and a variety of computing method (e.g. add, floating point) are embedded into controller to cope with commands from users. On the other hand, design in NTM controller only associates with architecture of neural network used inside. Strategies while confronting problems are not defined explicitly by engineers but can be learned through feeding input output pairs. In other word, ultimately, NTM can learn algorithms which may or may not be designed and developed by human.<br>
Furthermore, NTM is a neural network with memory. NTM has a explicitly-defined memory space, in which we can seperate “thinking” from “memory”, which is much similar to human brain. Also, apart from LSTM RNN, where memory is located implicitly and distributedly in the hidden state of each LSTM cell, centralized management over memory of NTM, in some cases, enjoy much faster training process. In certain intuition, imagine that we want to know the name of the host in a party. We can either try hard to learn from the hustle or simply jusk ask a person. 
</p>
##Read/Write Operation
###Read
<p>With normalized weighting vector Wt, we will get</p>
<p align="center">
<img src="img/normalized_weight_vector.png">
</p>
<p>If we have a row vector Mt in memory, then we define the read vector by multipliation with weighting vector and memory vector:
</p>
<p align="center"><img src="img/read_vector.png"></p>
<p>then rt is data we get.</p>

###Write
<p>
When we want to write data into memory, we split writing into two parts: erase and add operation. First, we will erase data in memory with an erase vector et:
</p>
<p align="center"><img src="img/erase_vector.png"></p>
<p>
Mt bar is the erased memory based value and we will add it by an add vector:
</p>
<p align="center"><img src="img/add_vector.png"></p>
<p>
The Mt will be the final value stored into memory.
</p>
##Addressing
<p>
In the previous part, we talked about the process of reading and writing of the memory. In this part, we will discuss about 
how the weight is produced to address the memory. There are two types of addressing: 
</p>
###Content based
<p>
Content based addressing relies on similarity between the output of controller and the content in the memory. As a result, it is relatively simple. 
</p>
###Location based
<p>
Location based is used in arithmatic operation. Since the content in such variable is arbitrary, the variable name is the one 
matters. Thus, similarity is of no use here.<br><br>
</p>
<p>
In Neural Turing Machine, it combined two types of addressing machanism to produce the weighting vector. The system flow diagram:
</p>
<p align="center"><img src="img/Flow_diagram.png"></p>
###Content Addressing
<p>In content addressing, we compare the output vector of controller with all the vectors stored in the memory.</p>
<p align="center"><img src="img/similarity_comparison.png"></p>
<p>kt is the output vector, ßt is a scalar deciding the precision of the focus, and K is the function producing cosine
similarity(like vector inner product):</p>
<p align="center"><img src="img/cosine.png"></p>

##Controller
<p>
ontroller is a neural network which will generate the representation that is used by read and write heads. Controller can be either a feed-foward network or a RNN.
</p>
###Type1, Feed-Forward
<p align="center"><img src="img/flow1.png"></p>
###Type2, RNN(LSTM)
<p align="center"><img src="img/flow2.png"></p>
