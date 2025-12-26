---
title: "MIT6.050J: Information theory and Entropy"
date: 2025-12-26T12:34:25+08:00
lastmod: 2025-12-26T14:54:22+08:00
math: true
categories:
- 在线课程
tags:
- MIT
- Infomation theory
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: ""
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
---


# 概论

## 前言

本课程内容还是挺丰富的，就是最后的量子信息部分内容不全。考虑到时代因素，这点是可以理解的。

## 课程简介

MIT6.050J: Information theory and Entropy

- 所属大学：MIT
- 先修要求：无
- 编程语言：无
- 课程难度：🌟🌟🌟
- 预计学时：100 小时

MIT 面向大一新生的信息论入门课程，Penfield 教授专门为这门课写了一本[教材](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-050j-information-and-entropy-spring-2008/syllabus/MIT6_050JS08_textbook.pdf)作为课程 notes，内容深入浅出，生动有趣。

## 课程资源

- 课程网站：[spring2008](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-050j-information-and-entropy-spring-2008/index.htm)
- 课程教材：[Information and Entropy](https://ocw.mit.edu/courses/6-050j-information-and-entropy-spring-2008/resources/mit6_050js08_textbook/)
- 课程作业：详见课程网站，包含书面作业与 Matlab 编程作业。

# 课程内容

## Preface

These notes, and the related freshman-level course, are about information. Although you may have a general idea of what information is, you may not realize that the information you deal with can be quantified. That’s right, you can often measure the amount of information and use general principles about how information behaves. We will consider applications to computation and to communications, and we will also look at general laws in other fields of science and engineering. 

One of these general laws is the Second Law of Thermodynamics. Although thermodynamics, a branch of physics, deals with physical systems, the Second Law is approached here as an example of information processing in natural and engineered systems. The Second Law as traditionally stated in thermodynamics deals with a physical quantity known as “entropy.” Everybody has heard of entropy, but few really understand it. Only recently has entropy been widely accepted as a form of information. 

The Second Law is surely one of science’s most glorious achievements, but as usually taught, through physical systems and models such as ideal gases, it is difficult to appreciate at an elementary level. On the other hand, the forms of the Second Law that apply to computation and communications (where information is processed) are more easily understood, especially today as the information revolution is getting under way. 

These notes and the course based on them are intended for first-year university students. Although they were developed at the Massachusetts Institute of Technology, a university that specializes in science and engineering, and one at which a full year of calculus is required, calculus is not used much at all in these notes. Most examples are from discrete systems, not continuous systems, so that sums and differences can be used instead of integrals and derivatives. In other words, we can use algebra instead of calculus. This course should be accessible to university students who are not studying engineering or science, and even to well prepared high-school students. In fact, when combined with a similar one about energy, this course could provide excellent science background for liberal-arts students. 

The analogy between information and energy is interesting. In both high-school and first-year college physics courses, students learn that there is a physical quantity known as energy which is conserved (it cannot be created or destroyed), but which can appear in various forms (potential, kinetic, electric, chemical, etc.). Energy can exist in one region of space or another, can flow from one place to another, can be stored for later use, and can be converted from one form to another. In many ways the industrial revolution was all about harnessing energy for useful purposes. But most important, energy is conserved—despite its being moved, stored, and converted, at the end of the day there is still exactly the same total amount of energy. 

This conservation of energy principle is sometimes known as the First Law of Thermodynamics. It has proven to be so important and fundamental that whenever a “leak” was found, the theory was rescued by defining a new form of energy. One example of this occurred in 1905 when Albert Einstein recognized that mass is a form of energy, as expressed by his famous formula $E = mc^2$. That understanding later enabled the development of devices (atomic bombs and nuclear power plants) that convert energy from its form as mass to other forms. 

But what about information? If entropy is really a form of information, there should be a theory that covers both and describes how information can be turned into entropy or vice versa. Such a theory is not yet well developed, for several historical reasons. Yet it is exactly what is needed to simplify the teaching and understanding of fundamental concepts. 

These notes present such a unified view of information, in which entropy is one kind of information, but in which there are other kinds as well. Like energy, information can reside in one place or another, it can be transmitted through space, and it can be stored for later use. But unlike energy, information is not conserved: the Second Law states that entropy never decreases as time goes on—it generally increases, but may in special cases remain constant. Also, information is inherently subjective, because it deals with what you know and what you don’t know (entropy, as one form of information, is also subjective—this point makes some physicists uneasy). These two facts make the theory of information different from theories that deal with conserved quantities such as energy—different and also interesting. 

The unified framework presented here has never before been developed specifically for freshmen. It is not entirely consistent with conventional thinking in various disciplines, which were developed separately. In fact, we may not yet have it right. One consequence of teaching at an elementary level is that unanswered questions close at hand are disturbing, and their resolution demands new research into the fundamentals. Trying to explain things rigorously but simply often requires new organizing principles and new approaches. In the present case, the new approach is to start with information and work from there to entropy, and the new organizing principle is the unified theory of information. 

This will be an exciting journey. Welcome aboard!

## Units 1: Bits

If Alice flipped two coins, she could say which of the four possible outcomes actually happened, by saying 0 or 1 twice. Similarly, the result of an experiment with eight equally likely outcomes could be conveyed with three bits, and more generally $2^n$ outcomes with n bits. Thus the amount of information is the logarithm (to the base 2) of the number of equally likely outcomes.

uncertainty, or lack of information

Note some important things about information, some of which are illustrated in this example: 

- Information can be learned through observation, experiment, or measurement
- Information is subjective, or “observer-dependent.” What Alice knows is different from what Bob knows (if information were not subjective, there would be no need to communicate it) 
- A person’s uncertainty can be increased upon learning that there is an observation about which information may be available, and then can be reduced by receiving that information 
- Information can be lost, either through loss of the data itself, or through loss of the code 
- The physical form of information is localized in space and time. As a consequence, 
	- Information can be sent from one place to another 
	- Information can be stored and then retrieved later

### 1.1 The Boolean Bit

![](https://setsailtowardstianhan.ip-ddns.com/blog/6aea4cae52cce7802f06a1aecdffe23f.png)

There is a standard notation used in Boolean algebra. (This notation is sometimes confusing, but other notations that are less confusing are awkward in practice.) The AND function is represented the same way as multiplication, by writing two Boolean values next to each other or with a dot in between: A AND B is written AB or A B· . The OR function is written using the plus sign: A + B means A OR B. Negation, or the NOT function, is denoted by a bar over the symbol or expression, so NOT A is A. Finally, the exclusive-or function XOR is represented by a circle with a plus sign inside, A ⊕ B.

There are other possible notations for Boolean algebra. The one used here is the most common. Sometimes AND, OR, and NOT are represented in the form AND(A, B), OR(A, B), and NOT(A). Sometimes infix notation is used where A ∧ B denotes A · B, A ∨ B denotes A + B, and ∼A denotes $\bar{A}$. Boolean algebra is also useful in mathematical logic, where the notation A ∧ B for A · B, A ∨ B for A + B, and ¬A for $\bar{A}$ is commonly used.

![](https://setsailtowardstianhan.ip-ddns.com/blog/748dc10ebe23e86fd79b7103f0f0877e.png)

### 1.2 The Circuit Bit 

Combinational logic circuits are a way to represent Boolean expressions graphically. Each Boolean function (NOT, AND, XOR, etc.) corresponds to a “combinational gate” with one or two inputs and one output, as shown in Figure 1.1. The different types of gates have different shapes. Lines are used to connect the output of one gate to one or more gate inputs, as illustrated in the circuits of Figure 1.2. 

Logic circuits are widely used to model digital electronic circuits, where the gates represent parts of an integrated circuit and the lines represent the signal wiring.

Combinational circuits have the property that the output from a gate is never fed back to the input of any gate whose output eventually feeds the input of the first gate. In other words, there are no loops in the circuit. Circuits with loops are known as sequential logic, and Boolean algebra is not sufficient to describe them. 

A model more complicated than Boolean algebra is needed to describe the behavior of sequential logic circuits. For example, the gates or the connecting lines (or both) could be modeled with time delays. The circuit at the bottom of Figure 1.3 (for example with 13 or 15 gates) is commonly known as a ring oscillator, and is used in semiconductor process development to test the speed of circuits made using a new process. 

### 1.3 The Control Bit

In computer programs, Boolean expressions are often used to determine the flow of control, i.e., which statements are executed. Suppose, for example, that if one variable x is negative and another y is positive, then a third variable z should be set to zero. In the language Scheme, the following statement would accomplish this: (if (and (< x 0) (> y 0)) (define z 0)) (other languages have their own ways of expressing the same thing). 

The algebra of control bits is like Boolean algebra with an interesting difference: any part of the control expression that does not affect the result may be ignored. In the case above (assuming the arguments of and are evaluated left to right), if x is found to be positive then the result of the and operation is 0 regardless of the value of y, so there is no need to see if y is positive or even to evaluate y. As a result the program can run faster, and side effects associated with evaluating y do not happen. 

### 1.4 The Physical Bit

If a bit is to be stored or transported, it must have a physical form. Whatever object stores the bit has two distinct states, one of which is interpreted as 0 and the other as 1. A bit is stored by putting the object in one of these states, and when the bit is needed the state of the object is measured. If the object has moved from one location to another without changing its state then communications has occurred. If the object has persisted over some time in its same state then it has served as a memory. If the object has had its state changed in a random way then its original value has been forgotten.

In keeping with the Engineering Imperative (make it smaller, faster, stronger, smarter, safer, cheaper),we are especially interested in physical objects that are small. The limit to how small an object can be and still store a bit of information comes from quantum mechanics. The quantum bit, or qubit, is a model of an object that can store a single bit but is so small that it is subject to the limitations quantum mechanics places on measurements. 

### 1.5 The Quantum Bit

According to quantum mechanics, it is possible for a small object to have two states which can be measured. This sounds perfect for storing bits, and the result is often called a qubit, pronounced “cue-bit.” The two values are often denoted $|0>$ and $|1>$ rather than 0 and 1, because this notation generalizes to what is needed to represent more than one qubit, and it avoids confusion with the real numbers 0 and 1. There are three features of quantum mechanics, reversibility, superposition, and entanglement, that make qubits or collections of qubits different from Boolean bits.

The polarization can be used to store a bit of information.

Note that quantum systems don’t always exhibit the peculiarities associated with superposition and entanglement. For example, photons can be prepared independently (so there is no entanglement) and the angles of polarization can be constrained to be horizontal and vertical (no superposition). In this case qubits behave like Boolean bits.

This scenario relies on the quantum nature of the photons, and the fact that single photons cannot be measured by Sam except along particular angles of polarization. Thus Alice’s technique for thwarting Sam is not possible with classical bits.

### 1.6 The Classical Bit

Because quantum measurement generally alters the object being measured, a quantum bit cannot be measured a second time. On the other hand, if a bit is represented by many objects with the same properties, then after a measurement enough objects can be left unchanged so that the same bit can be measured again.

Circuits of this sort display what is known as “restoring logic” since small deviations in voltage from the ideal values of 0V and 1V are eliminated as the information is processed. The robustness of modern computers depends on the use of restoring logic. 

A classical bit is an abstraction in which the bit can be measured without perturbing it. As a result copies of a classical bit can be made. This model works well for circuits using restoring logic. 

Because all physical systems ultimately obey quantum mechanics, the classical bit is always an approximation to reality. However, even with the most modern, smallest devices available, it is an excellent one. An interesting question is whether the classical bit approximation will continue to be useful as advances in semiconductor technology allow the size of components to be reduced. Ultimately, as we try to represent or control bits with a small number of atoms or photons, the limiting role of quantum mechanics will become important. It is difficult to predict exactly when this will happen, but some people believe it will be before the year 2015. 

### 1.7 Summary 

There are several models of a bit, useful in different contexts. These models are not all the same. In the rest of these notes, the Boolean bit will be used most often, but sometimes the quantum bit will be needed.
## Units 2: Codes

In the previous chapter we examined the fundamental unit of information, the bit, and its various abstract representations: the Boolean bit (with its associated Boolean algebra and realization in combinational logic circuits), the control bit, the quantum bit, and the classical bit. 

A single bit is useful if exactly two answers to a question are possible. Examples include the result of a coin toss (heads or tails), the gender of a person (male or female), the verdict of a jury (guilty or not guilty), and the truth of an assertion (true or false). Most situations in life are more complicated. This chapter concerns ways in which complex objects can be represented not by a single bit, but by arrays of bits. 

It is convenient to focus on a very simple model of a system, shown in Figure 2.1, in which the input is one of a predetermined set of objects, or “symbols,” the identity of the particular symbol chosen is encoded in an array of bits, these bits are transmitted through space or time, and then are decoded at a later time or in a different place to determine which symbol was originally chosen. In later chapters we will augment this model to deal with issues of robustness and efficiency. 

![](https://setsailtowardstianhan.ip-ddns.com/blog/56cb55c24dc3342ef76fbe025c0f9096.png)

Figure 2.1: Simple model of a communication system 

In this chapter we will look into several aspects of the design of codes, and show some examples in which these aspects were either done well or not so well. Individual sections will describe codes that illustrate the important points. Some objects for which codes may be needed include: 

- Letters: BCD, EBCDIC, ASCII, Unicode, Morse Code 
- Integers: Binary, Gray, 2’s complement
- Numbers: Floating-Point 
- Proteins: Genetic Code
- Telephones: NANP, International codes
- Hosts: Ethernet, IP Addresses, Domain names 
- Images: TIFF, GIF, and JPEG 
- Audio: MP3 
- Video: MPEG

### 2.1 Symbol Space Size 

The first question to address is the number of symbols that need to be encoded. This is called the symbol space size.

### 2.2 Use of Spare Capacity 

In many situations there are some unused code patterns, because the number of symbols is not an integral power of 2. There are many strategies to deal with this. Here are some: 

- Ignore 
- Map to other values 
- Reserve for future expansion 
- Use for control codes 
- Use for common abbreviations 

These approaches will be illustrated with examples of common codes.

#### 2.2.1 Binary Coded Decimal (BCD) 

A common way to represent the digits 0 - 9 is by the ten four-bit patterns shown in Table 2.1. There are six bit patterns (for example 1010) that are not used, and the question is what to do with them. Here are a few ideas that come to mind.

#### 2.2.2 Genetic Code

The Genetic Code is a description of how a sequence of nucleotides specifies an amino acid. Given that relationship, an entire protein can be specified by a linear sequence of nucleotides. Note that the coded description of a protein is not by itself any smaller or simpler than the protein itself; in fact, the number of atoms needed to specify a protein is larger than the number of atoms in the protein itself. The value of the standardized representation is that it allows the same assembly apparatus to fabricate different proteins at different times

Since there are four different nucleotides, one of them can specify at most four different amino acids. A sequence of two can specify 16 different amino acids. But this is not enough – there are 20 different amino acids used in proteins – so a sequence of three is needed. Such a sequence is called a codon. There are 64 different codons, more than enough to specify 20 amino acids. The spare capacity is used to provide more than one combination for most amino acids, thereby providing a degree of robustness. For example, the amino acid Alanine has 4 codes including all that start with GC; thus the third nucleotide can be ignored, so a mutation which changed it would not impair any biological functions. In fact, eight of the 20 amino acids have this same property that the third nucleotide is a “don’t care.” (It happens that the third nucleotide is more likely to be corrupted during transcription than the other two, due to an effect that has been called “wobble.”) 

An examination of the Genetic Code reveals that three codons (UAA, UAG, and UGA) do not specify any amino acid. These three signify the end of the protein. Such a “stop code” is necessary because different proteins are of different length. The codon AUG specifies the amino acid Methionine and also signifies the beginning of a protein; all protein chains begin with Methionine. Many man-made codes have this property, that some bit sequences designate data but a few are reserved for control information. 

#### 2.2.3 Telephone Area Codes 

The third way in which spare capacity can be used is by reserving it for future expansion. When AT&T started using telephone Area Codes for the United States and Canada in 1947 (they were made available for public use in 1951), the codes contained three digits, with three restrictions.

#### 2.2.4 IP Addresses

Another example of the need to reserve capacity for future use is afforded by IP (Internet Protocol) addresses, which is described in Section 2.8. These are (in version 4) of the form x.x.x.x where each x is a number between 0 and 255, inclusive. Thus each Internet address can be coded in a total of 32 bits. IP addresses are assigned by the Internet Assigned Numbers Authority, http://www.iana.org/, (IANA).

#### 2.2.5 ASCII 

A fourth use for spare capacity in codes is to use some of it for denoting formatting or control operations. Many codes incorporate code patterns that are not data but control codes. For example, the Genetic Code includes three patterns of the 64 as stop codes to terminate the production of the protein. 

The most commonly used code for text characters, ASCII (American Standard Code for Information Interchange, described in Section 2.5) reserves 33 of its 128 codes explicitly for control, and only 95 for characters. These 95 include the 26 upper-case and 26 lower-case letters of the English alphabet, the 10 digits, space, and 32 punctuation marks.

### 2.4 Fixed-Length and Variable-Length Codes

A decision that must be made very early in the design of a code is whether to represent all symbols with codes of the same number of bits (fixed length) or to let some symbols use shorter codes than others (variable length). There are advantages to both schemes.

#### 2.4.1 Morse Code

An example of a variable-length code is Morse Code, developed for the telegraph. The codes for letters, digits, and punctuation are sequences of dots and dashes with short-length intervals between them. See Section 2.9. 

The decoder tells the end of the code for a single character by noting the length of time before the next dot or dash. The intra-character separation is the length of a dot, and the inter-character separation is longer, the length of a dash. The inter-word separation is even longer.

### 2.5 Detail: ASCII 

ASCII, which stands for “The American Standard Code for Information Interchange,” was introduced by the American National Standards Institute (ANSI) in 1963. It is the most commonly used character code.

#### On to 8 Bits 

In an 8-bit context, ASCII characters follow a leading 0, and thus may be thought of as the “bottom half” of a larger code.
#### Beyond 8 Bits

To represent Asian languages, many more characters are needed. There is currently active development of appropriate standards, and it is generally felt that the total number of characters that need to be represented is less that 65,536. This is fortunate because that many different characters could be represented in 16 bits, or 2 bytes. In order to stay within this number, the written versions of some of the Chinese dialects must share symbols that look alike. 

The strongest candidate for a 2-byte standard character code today is known as Unicode.

### 2.6 Detail: Integer Codes 

There are many ways to represent integers as bit patterns. All suffer from an inability to represent arbitrarily large integers in a fixed number of bits. A computation which produces an out-of-range result is said to overflow. 

The most commonly used representations are binary code for unsigned integers (e.g., memory addresses), 2’s complement for signed integers (e.g., ordinary arithmetic), and binary gray code for instruments measuring changing quantities. 

The following table gives five examples of 4-bit integer codes. The MSB (most significant bit) is on the left and the LSB (least significant bit) on the right.

常见整数编码类型：

- Binary Code
- Binary Gray Code
- 2’s Complement
- Sign/Magnitude
- 1’s Complement

### 2.7 Detail: The Genetic Code∗

### 2.8 Detail: IP Addresses 

Table 2.7 is an excerpt from IPv4, http://www.iana.org/assignments/ipv4-address-space (version 4, which is in the process of being phased out in favor of version 6). IP addresses are assigned by the Internet Assigned Numbers Authority (IANA), http://www.iana.org/. 

IANA is in charge of all “unique parameters” on the Internet, including IP (Internet Protocol) addresses. Each domain name is associated with a unique IP address, a numerical name consisiting of four blocks of up to three digits each, e.g. 204.146.46.8, which systems use to direct information through the network.

### 2.9 Detail: Morse Code

Samuel F. B. Morse (1791–1872) was a landscape and portrait painter from Charleston, MA. He frequently travelled from his studio in New York City to work with clients across the nation. He was in Washington, DC in 1825 when his wife Lucretia died suddenly of heart failure. Morse learned of this event as rapidly as was possible at the time, through a letter sent from New York to Washington, but it was too late for him to return in time for her funeral.

Morse Code consists of a sequence of short and long pulses or tones (dots and dashes) separated by short periods of silence. A person generates Morse Code by making and breaking an electrical connection on a hand key, and the person on the other end of the line listens to the sequence of dots and dashes and converts them to letters, spaces, and punctuation. The modern form of Morse Code is shown in Table 2.8. The at sign was added in 2004 to accommodate email addresses. Two of the dozen or so control codes are shown. Non-English letters and some of the less used punctuation marks are omitted.

![](https://setsailtowardstianhan.ip-ddns.com/blog/523a7232d2430fe3a5451c3ffe0d17a3.png)

A comparison of Tables 2.8 and 2.9 reveals that Morse did a fairly good job of assigning short sequences to the more common letters. It is reported that he did this not by counting letters in books and newspapers, but by visiting a print shop. The printing presses at the time used movable type, with separate letters assembled by humans into lines. Each letter was available in multiple copies for each font and size, in the form of pieces of lead. Morse simply counted the pieces of type available for each letter of the alphabet, assuming that the printers knew their business and stocked their cases with the right quantity of each letter. The wooden type cases were arranged with two rows, the capital letters in the upper one and small letters in the lower one. Printers referred to those from the upper row of the case as “uppercase” letters.
## Unit 3: Compression

Typically the same code is used for a sequence of symbols, one after another. The role of data compression is to convert the string of bits representing a succession of symbols into a shorter string for more economical transmission, storage, or processing. The result is the system in Figure 3.2, with both a compressor and an expander. Ideally, the expander would exactly reverse the action of the compressor so that the coder and decoder could be unchanged.

On first thought, this approach might seem surprising. Why is there any reason to believe that the same information could be contained in a smaller number of bits? We will look at two types of compression, using different approaches: 

- Lossless or reversible compression (which can only be done if the original code was inefficient, for example by having unused bit patterns, or by not taking advantage of the fact that some symbols are used more frequently than others) 
- Lossy or irreversible compression, in which the original symbol, or its coded representation, cannot be reconstructed from the smaller version exactly, but instead the expander produces an approximation that is “good enough” 

Six techniques are described below which are astonishingly effective in compressing data files. The first five are reversible, and the last one is irreversible. Each technique has some cases for which it is particularly well suited (the best cases) and others for which it is not well suited (the worst cases).

### 3.1 Variable-Length Encoding

### 3.2 Run Length Encoding

Suppose a message consists of long sequences of a small number of symbols or characters. Then the message could be encoded as a list of the symbol and the number of times it occurs. For example, the message “a B B B B B a a a B B a a a a” could be encoded as “a 1 B 5 a 3 B 2 a 4”. This technique works very well for a relatively small number of circumstances.

### 3.3 Static Dictionary

The list of the codewords and their meanings is called a codebook, or dictionary. The compression technique considered here uses a dictionary which is static in the sense that it does not change from one message to the next.

### 3.4 Semi-adaptive Dictionary

The static-dictionary approach requires one dictionary, defined in advance, that applies to all messages. If a new dictionary could be defined for each message, the compression could be greater because the particular sequences of symbols found in the message could be made into dictionary entries.

### 3.5 Dynamic Dictionary 

What would be best for many applications would be an encoding scheme using a dictionary that is calculated on the fly, as the message is processed, does not need to accompany the message, and can be used before the end of the message has been processed. On first consideration, this might seem impossible. However, such a scheme is known and in wide use. It is the LZW compression technique, named after Abraham Lempel, Jacob Ziv, and Terry Welch. Lempel and Ziv actually had a series of techniques, sometimes referred to as LZ77 and LZ78, but the modification by Welch in 1984 gave the technique all the desired characteristics.

The commonly used GIF image format uses LZW compression. When used with photographs, with their gradual changes of color, the savings are much more modest. 

Because this is a reversible compression technique, the original data can be reconstructed exactly, without approximation, by the decoder. 

The LZW technique seems to have many advantages. However, it had one major disadvantage. It was not freely available—it was patented. The U.S. patent, No. 4,558,302, expired June 20, 2003, and patents in other countries in June, 2004, but before it did, it generated a controversy that is still an unpleasant memory for many because of the way it was handled.

A non-infringing public-domain image-compression standard called PNG was created to replace GIF, but the browser manufacturers were slow to adopt yet another image format. Also, everybody knew that the patents would expire soon. The controversy has now gone away except in the memory of a few who felt particularly strongly. It is still cited as justification for or against changes in the patent system, or even the concept of software patents in general. 

As for PNG, it offers some technical advantages (particularly better transparency features) and, as of 2004, was well supported by almost all browsers, the most significant exception being Microsoft Internet Explorer for Windows.

### 3.6 Irreversible Techniques

This section is not yet available. Sorry. 

It will include as examples floating-point numbers, JPEG image compression, and MP3 audio compression. The Discrete Cosine Transformation (DCT) used in JPEG compression is discussed in Section 3.8. A demonstration of MP3 compression is available at http://www.mtl.mit.edu/Courses/6.050/2007/notes/mp3.html.

### 3.7 Detail: LZW Compression

The LZW compression technique is described below and applied to two examples. Both encoders and decoders are considered. The LZW compression algorithm is “reversible,” meaning that it does not lose any information—the decoder can reconstruct the original message exactly.

### 3.8 Detail: 2-D Discrete Cosine Transformation

This section is based on notes written by Luis P´erez-Breva, Feb 3, 2005, and notes from Joseph C. Huang, Feb 25, 2000. 

The Discrete Cosine Transformation (DCT) is an integral part of the JPEG (Joint Photographic Experts Group) compression algorithm. DCT is used to convert the information in an array of picture elements (pixels) into a form in which the information that is most relevant for human perception can be identified and retained, and the information less relevant may be discarded. 

DCT is one of many discrete linear transformations that might be considered for image compression. It has the advantage that fast algorithms (related to the FFT, Fast Fourier Transform) are available. 

Several mathematical notations are possible to describe DCT. The most succinct is that using vectors and matrices. A vector is a one-dimensional array of numbers (or other things). It can be denoted as a single character or between large square brackets with the individual elements shown in a vertical column (a row representation, with the elements arranged horizontally, is also possible, but is usually regarded as the transpose of the vector). In these notes we will use bold-face letters (V) for vectors. A matrix is a two-dimensional array of numbers (or other things) which again may be represented by a single character or in an array between large square brackets. In these notes we will use a font called “blackboard bold” (M) for matrices. When it is necessary to indicate particular elements of a vector or matrix, a symbol with one or two subscripts is used. In the case of a vector, the single subscript is an integer in the range from 0 through n − 1 where n is the number of elements in the vector. In the case of a matrix, the first subscript denotes the row and the second the column, each an integer in the range from 0 through n − 1 where n is either the number of rows or the number of columns, which are the same only if the matrix is square.

#### 3.8.1 Discrete Linear Transformations

#### 3.8.2 Discrete Cosine Transformation


## Unit 4: Noise and Errors

In Chapter 2 we saw examples of how symbols could be represented by arrays of bits. In Chapter 3 we looked at some techniques of compressing the bit representations of such symbols, or a series of such symbols, so fewer bits would be required to represent them. If this is done while preserving all the original information, the compressions are said to be lossless, or reversible, but if done while losing (presumably unimportant) information, the compression is called lossy, or irreversible. Frequently source coding and compression are combined into one operation. 

Because of compression, there are fewer bits carrying the same information, so each bit is more important, and the consequence of an error in a single bit is more serious. All practical systems introduce errors to information that they process (some systems more than others, of course). In this chapter we examine techniques for insuring that such inevitable errors cause no harm.

### 4.1 Extension of System Model

Our model for information handling will be extended to include “channel coding.” The new channel encoder adds bits to the message so that in case it gets corrupted in some way, the channel encoder will know that and possibly even be able to repair the damage.

![](https://setsailtowardstianhan.ip-ddns.com/blog/29d983e1b8c07bb1e3b30ad4c578e4f8.png)

### 4.2 How do Errors Happen? 

The model pictured above is quite general, in that the purpose might be to transmit information from one place to another (communication), store it for use later (data storage), or even process it so that the output is not intended to be a faithful replica of the input (computation). Different systems involve different physical devices as the channel (for example a communication link, a floppy disk, or a computer). Many physical effects can cause errors. A CD or DVD can get scratched. A memory cell can fail. A telephone line can be noisy. A computer gate can respond to an unwanted surge in power supply voltage. 

For our purposes we will model all such errors as a change in one or more bits from 1 to 0 or vice versa. In the usual case where a message consists of several bits, we will usually assume that different bits get corrupted independently, but in some cases errors in adjacent bits are not independent of each other, but instead have a common underlying cause (i.e., the errors may happen in bursts). 

### 4.3 Detection vs. Correction 

There are two approaches to dealing with errors. One is to detect the error and then let the person or system that uses the output know that an error has occurred. The other is to have the channel decoder attempt to repair the message by correcting the error. In both cases, extra bits are added to the messages to make them longer. The result is that the message contains redundancy—if it did not, every possible bit pattern would be a legal message and an error would simply change one valid message to another. By changing things so that many (indeed, most) bit patterns do not correspond to legal messages, the effect of an error is usually to change the message to one of the illegal patterns; the channel decoder can detect that there was an error and take suitable action. In fact, if every illegal pattern is, in a sense to be described below, closer to one legal message than any other, the decoder could substitute the closest legal message, thereby repairing the damage. 

In everyday life error detection and correction occur routinely. Written and spoken communication is done with natural languages such as English, and there is sufficient redundancy (estimated at 50%) so that even if several letters, sounds, or even words are omitted, humans can still understand the message. 

Note that channel encoders, because they add bits to the pattern, generally preserve all the original information, and therefore are reversible. The channel, by allowing errors to occur, actually introduces information (the details of exactly which bits got changed). The decoder is irreversible in that it discards some information, but if well designed it throws out the “bad” information caused by the errors, and keeps the original information. In later chapters we will analyze the information flow in such systems quantitatively. 

### 4.4 Hamming Distance 

We need some technique for saying how similar two bit patterns are. In the case of physical quantities such as length, it is quite natural to think of two measurements as being close, or approximately equal. Is there a similar sense in which two patterns of bits are close? 

At first it is tempting to say that two bit patterns are close if they represent integers that are adjacent, or floating point numbers that are close. However, this notion is not useful because it is based on particular meanings ascribed to the bit patterns. It is not obvious that two bit patterns which differ in the first bit should be any more or less “different” from each other than two which differ in the last bit.

A more useful definition of the difference between two bit patterns is the number of bits that are different between the two. This is called the Hamming distance, after Richard W. Hamming (1915 – 1998). Thus 0110 and 1110 are separated by Hamming distance of one. Two patterns which are the same are separated by Hamming distance of zero.

Note that a Hamming distance can only be defined between two bit patterns with the same number of bits. It does not make sense to speak of the Hamming distance of a single string of bits, or between two bit strings of different lengths.

### 4.5 Single Bits 

Transmission of a single bit may not seem important, but it does bring up some commonly used techniques for error detection and correction. 

The way to protect a single bit is to send it more than once, and expect that more often than not each bit sent will be unchanged. The simplest case is to send it twice. Thus the message 0 is replaced by 00 and 1 by 11 by the channel encoder. The decoder can then raise an alarm if the two bits are different (that can only happen because of an error). But there is a subtle point. What if there are two errors? If the two errors both happen on the same bit, then that bit gets restored to its original value and it is as though no error happened. But if the two errors happen on different bits then they end up the same, although wrong, and the error is undetected. If there are more errors, then the possibility of undetected changes becomes substantial (an odd number of errors would be detected but an even number would not). 

If multiple errors are likely, greater redundancy can help. Thus, to detect double errors, you can send the single bit three times. Unless all three are the same when received by the channel decoder, it is known that an error has occurred, but it is not known how many errors there might have been. And of course triple errors may go undetected. 

Now what can be done to allow the decoder to correct an error, not just detect one? If there is known to be at most one error, and if a single bit is sent three times, then the channel decoder can tell whether an error has occurred (if the three bits are not all the same) and it can also tell what the original value was—the process used is sometimes called “majority logic” (choosing whichever bit occurs most often). This technique, called ”triple redundancy” can be used to protect communication channels, memory, or arbitrary computation. 

Note that triple redundancy can be used either to correct single errors or to detect double errors, but not both. If you need both, you can use quadruple redundancy—send four identical copies of the bit. 

Two important issues are how efficient and how effective these techniques are. As for efficiency, it is convenient to define the code rate as the number of bits before channel coding divided by the number after the encoder. Thus the code rate lies between 0 and 1. Double redundancy leads to a code rate of 0.5, and triple redundancy 0.33. As for effectiveness, if errors are very unlikely it may be reasonable to ignore the even more unlikely case of two errors so close together. If so, triple redundancy is very effective. On the other hand, some physical sources of errors may wipe out data in large bursts (think of a physical scratch on a CD) in which case one error, even if unlikely, is apt to be accompanied by a similar error on adjacent bits, so triple redundancy will not be effective.

### 4.6 Multiple Bits 

To detect errors in a sequence of bits several techniques can be used. Some can perform error correction as well as detection.

#### 4.6.1 Parity（奇偶校验）

Error correction is more useful than error detection, but requires more bits and is therefore less efficient. Two of the more common methods are discussed next.

#### 4.6.2 Rectangular Codes

Rectangular codes can provide single error correction and double error detection simultaneously.

#### 4.6.3 Hamming Codes 

Suppose we wish to correct single errors, and are willing to ignore the possibility of multiple errors. A set of codes was invented by Richard Hamming with the minimum number of extra parity bits.

Each extra bit added by the channel encoder allows one check of a parity by the decoder and therefore one bit of information that can be used to help identify the location of the error. For example, if three extra bits are used, the three tests could identify up to eight error conditions. One of these would be “no error” so seven would be left to identify the location of up to seven places in the pattern with an error. Thus the data block could be seven bits long. Three of these bits would be added for error checking, leaving four for the payload data. Similarly, if there were four parity bits, the block could be 15 bits long leaving 11 bits for payload.

### 4.7 Block Codes 

It is convenient to think in terms of providing error-correcting protection to a certain amount of data and then sending the result in a block of length n. If the number of data bits in this block is k, then the number of parity bits is n−k, and it is customary to call such a code an (n, k) block code. Thus the Hamming Code just described is (7, 4). 

It is also customary (and we shall do so in these notes) to include in the parentheses the minimum Hamming distance d between any two valid codewords, or original data items, in the form (n, k, d). The Hamming Code that we just described can then be categorized as a (7, 4, 3) block code. 

### 4.8 Advanced Codes

Block codes with minimum Hamming distance greater than 3 are possible. They can handle more than single errors. Some are known as Bose-Chaudhuri-Hocquenhem (BCH) codes. Of great commercial interest today are a class of codes announced in 1960 by Irving S. Reed and Gustave Solomon of MIT Lincoln Laboratory. These codes deal with bytes of data rather than bits. The (256, 224, 5) and (224, 192, 5) Reed-Solomon codes are used in CD players and can, together, protect against long error bursts. 

More advanced channel codes make use of past blocks of data as well as the present block. Both the encoder and decoder for such codes need local memory but not necessarily very much. The data processing for such advanced codes can be very challenging. It is not easy to develop a code that is efficient, protects against large numbers of errors, is easy to program, and executes rapidly. One important class of codes is known as convolutional codes, of which an important sub-class is trellis codes which are commonly used in data modems.

### 4.9 Detail: Check Digits

Error detection is routinely used to reduce human error. Many times people must deal with long serial numbers or character sequences that are read out loud or typed at a keyboard. Examples include credit-card numbers, social security numbers, and software registration codes. These actions are prone to error. Extra digits or characters can be included to detect errors, just as parity bits are included in bit strings. Often this is sufficient because when an error is detected the operation can be repeated conveniently. 

In other cases, such as telephone numbers or e-mail addresses, no check characters are used, and therefore any sequence may be valid. Obviously more care must be exercised in using these, to avoid dialing a wrong number or sending an e-mail message or fax to the wrong person.

- Credit Cards
- ISBN
- ISSN
## Unit 5: Probability

We consider only cases with a finite number of symbols to choose from, and only cases in which the symbols are both mutually exclusive (only one can be chosen at a time) and exhaustive (one is actually chosen). Each choice constitutes an “outcome” and our objective is to trace the sequence of outcomes, and the information that accompanies them, as the information travels from the input to the output. To do that, we need to be able to say what the outcome is, and also our knowledge about some properties of the outcome. 

If we know the outcome, we have a perfectly good way of denoting the result. We can simply name the symbol chosen, and ignore all the rest of the symbols, which were not chosen. But what if we do not yet know the outcome, or are uncertain to any degree? How are we supposed to express our state of knowledge if there is uncertainty? We will use the mathematics of probability for this purpose.

Statistics and probabilities can both be described using the same mathematics (to be developed next), but they are different things.

### 5.1 Events

Like many branches of mathematics or science, probability theory has its own nomenclature in which a word may mean something different from or more specific than its everyday meaning. Consider the two words event, which has several everyday meanings, and outcome. Merriam-Webster’s Collegiate Dictionary gives these definitions that are closest to the technical meaning in probability theory: 

• outcome: something that follows as a result or consequence 

• event: a subset of the possible outcomes of an experiment 

In our context, outcome is the symbol selected, whether or not it is known to us. While it is wrong to speak of the outcome of a selection that has not yet been made, it is all right to speak of the set of possible outcomes of selections that are contemplated. In our case this is the set of all symbols. As for the term event, its most common everyday meaning, which we do not want, is something that happens. Our meaning, which is quoted above, is listed last in the dictionary. We will use the word in this restricted way because we need a way to estimate or characterize our knowledge of various properties of the symbols. These properties are things that either do or do not apply to each symbol, and a convenient way to think of them is to consider the set of all symbols being divided into two subsets, one with that property and one without. When a selection is made, then, there are several events. One is the outcome itself. This is called a fundamental event. Others are the selection of a symbol with particular properties. 

Even though, strictly speaking, an event is a set of possible outcomes, it is common in probability theory to call the experiments that produce those outcomes events. Thus we will sometimes refer to a selection as an event. 

For example, suppose an MIT freshman is selected. The specific person chosen is the outcome. The fundamental event would be that person, or the selection of that person. Another event would be the selection of a woman (or a man). Another event might be the selection of someone from California, or someone older than 18, or someone taller than six feet. More complicated events could be considered, such as a woman from Texas, or a man from Michigan with particular SAT scores. 

The special event in which any symbol at all is selected, is certain to happen. We will call this event the universal event, after the name for the corresponding concept in set theory. The special “event” in which no symbol is selected is called the null event. The null event cannot happen because an outcome is only defined after a selection is made. 

Different events may or may not overlap, in the sense that two or more could happen with the same outcome. A set of events which do not overlap is said to be mutually exclusive. For example, the two events that the freshman chosen is (1) from Ohio, or (2) from California, are mutually exclusive. 

Several events may have the property that at least one of them happens when any symbol is selected. A set of events, one of which is sure to happen, is known as exhaustive. For example, the events that the freshman chosen is (1) younger than 25, or (2) older than 17, are exhaustive, but not mutually exclusive. 

A set of events that are both mutually exclusive and exhaustive is known as a partition. The partition that consists of all the fundamental events will be called the fundamental partition. In our example, the two events of selecting a woman and selecting a man form a partition, and the fundamental events associated with each of the 1073 personal selections form the fundamental partition. 

A partition consisting of a small number of events, some of which may correspond to many symbols, is known as a coarse-grained partition whereas a partition with many events is a fine-grained partition. The fundamental partition is as fine-grained as any. The partition consisting of the universal event and the null event is as coarse-grained as any. 

Although we have described events as though there is always a fundamental partition, in practice this partition need not be used.

### 5.2 Known Outcomes

### 5.3 Unknown Outcomes

### 5.4 Joint Events and Conditional Probabilities

p(A, B) = p(B)p(A | B) = p(A)p(B | A)

This formula is known as Bayes’ Theorem, after Thomas Bayes, the eighteenth century English mathematician who first articulated it. We will use Bayes’ Theorem frequently. This theorem has remarkable generality. It is true if the two events are physically or logically related, and it is true if they are not. It is true if one event causes the other, and it is true if that is not the case. It is true if the outcome is known, and it is true if the outcome is not known.

### 5.5 Averages

### 5.6 Information 

We want to express quantitatively the information we have or lack about the choice of symbol. After we learn the outcome, we have no uncertainty about the symbol chosen or about its various properties, and which events might have happened as a result of this selection. However, before the selection is made or at least before we know the outcome, we have some uncertainty. How much?

If we want to quantify our uncertainty before learning an outcome, we cannot use any of the information gained by specific outcomes, because we would not know which to use. Instead, we have to average over all possible outcomes, i.e., over all events in the partition with nonzero probability. The average information per event is found by multiplying the information for each event $A_i$ by $p(A_i)$ and summing over the partition: 

![](https://setsailtowardstianhan.ip-ddns.com/blog/336033722dd27ce37c568cee6199efe0.png)

This quantity, which is of fundamental importance for characterizing the information of sources, is called the entropy of a source. The formula works if the probabilities are all equal and it works if they are not; it works after the outcome is known and the probabilities adjusted so that one of them is 1 and all the others 0; it works whether the events being reported are from a fundamental partition or not. 

In this and other formulas for information, care must be taken with events that have zero probability. These cases can be treated as though they have a very small but nonzero probability. In this case the logarithm, although it approaches infinity for an argument approaching infinity, does so very slowly. The product of that factor times the probability approaches zero, so such terms can be directly set to zero even though the formula might suggest an indeterminate result, or a calculating procedure might have a “divide by zero” error.

### 5.7 Properties of Information

### 5.8 Efficient Source Coding

Certainly. Morse Code is an example of a variable length code which does this quite well. There is a general procedure for constructing codes of this sort which are very efficient (in fact, they require an average of less than $I +1$ bits per symbol, even if I is considerably below $log_2(n)$. The codes are called Huffman codes after MIT graduate David Huffman (1925 - 1999), and they are widely used in communication systems. See Section 5.10.

### 5.9 Detail: Life Insurance

### 5.10 Detail: Efficient Source Code 

Sometimes source coding and compression for communication systems of the sort shown in Figure 5.1 are done together (it is an open question whether there are practical benefits to combining source and channel coding). For sources with a finite number of symbols, but with unequal probabilities of appearing in the input stream, there is an elegant, simple technique for source coding with minimum redundancy

#### Huffman Code 

David A. Huffman (August 9, 1925 - October 6, 1999) was a graduate student at MIT. To solve a homework assignment for a course he was taking from Prof. Robert M. Fano, he devised a way of encoding symbols with different probabilities, with minimum redundancy and without special symbol frames, and hence most compactly. He described it in Proceedings of the IRE, September 1962. His algorithm is very simple. The objective is to come up with a “codebook” (a string of bits for each symbol) so that the average code length is minimized. Presumably infrequent symbols would get long codes, and common symbols short codes, just like in Morse code. The algorithm is as follows (you can follow along by referring to Table 5.5): 

1. Initialize: Let the partial code for each symbol initially be the empty bit string. Define corresponding to each symbol a “symbol-set,” with just that one symbol in it, and a probability equal to the probability of that symbol. 
2. Loop-test: If there is exactly one symbol-set (its probability must be 1) you are done. The codebook consists of the codes associated with each of the symbols in that symbol-set. 
3. Loop-action: If there are two or more symbol-sets, take the two with the lowest probabilities (in case of a tie, choose any two). Prepend the codes for those in one symbol-set with 0, and the other with 1. Define a new symbol-set which is the union of the two symbol-sets just processed, with probability equal to the sum of the two probabilities. Replace the two symbol-sets with the new one. The number of symbol-sets is thereby reduced by one. Repeat this loop, including the loop test, until only one symbol-set remains. 

Note that this procedure generally produces a variable-length code. If there are n distinct symbols, at least two of them have codes with the maximum length.

#### Another Example

Freshmen at MIT are on a “pass/no-record” system during their first semester on campus.

Huffman coding on single symbols does not help.
## Unit 6: Communications

In this chapter we focus on how fast the information that identifies the symbols can be transferred to the output. The symbols themselves, of course, are not transmitted, but only the information necessary to identify them. This is what is necessary for the stream of symbols to be recreated at the output. 

We will model both the source and the channel in a little more detail, and then give three theorems relating to the source characteristics and the channel capacity. 

### 6.1 Source Model 

The source is assumed to produce symbols at a rate of R symbols per second.

An important property of such codewords is that none can be the same as the first portion of another, longer, codeword—otherwise the same bit pattern might result from two or more different messages, and there would be ambiguity. A code that obeys this property is called a prefix-condition code, or sometimes an instantaneous code. 

#### 6.1.1 Kraft Inequality 

Since the number of distinct codes of short length is limited, not all codes can be short. Some must be longer, but then the prefix condition limits the available short codes even further. An important limitation on the distribution of code lengths Li was given by L. G. Kraft, an MIT student, in his 1949 Master’s thesis. It is known as the Kraft inequality: 

$$\sum \frac{1}{2^{L_i}} \leq 1$$

Any valid set of distinct codewords obeys this inequality, and conversely for any proposed Li that obey it, a code can be found.

### 6.2 Source Entropy 

As part of the source model, we assume that each symbol selection is independent of the other symbols chosen, so that the probability p(Ai) does not depend on what symbols have previously been chosen (this model can, of course, be generalized in many ways). The uncertainty of the identity of the next symbol chosen H is the average information gained when the next symbol is made known: 

$$H = \sum_i p(A_i)log_2(\frac{1}{p(A_i)})$$

This quantity is also known as the entropy of the source, and is measured in bits per symbol. The information rate, in bits per second, is H R· where R is the rate at which the source selects the symbols, measured in symbols per second. 

#### 6.2.1 Gibbs Inequality 

Here we present the Gibbs Inequality, named after the American physicist J. Willard Gibbs (1839–1903)1, which will be useful to us in later proofs. This inequality states that the entropy is smaller than or equal to any other average formed using the same probabilities but a different function in the logarithm. Specifically,

$$\sum_i p(A_i)log_2(\frac{1}{p(A_i)}) \leq \sum_i p(A_i)log_2(\frac{1}{p'(A_i)})$$

### 6.3 Source Coding Theorem 

Now getting back to the source model, note that the codewords have an average length, in bits per symbol, 

$$L = \sum_i p(A_i)L_i$$
For maximum speed the lowest possible average codeword length is needed. The assignment of high-probability symbols to the short codewords can help make L small. Huffman codes are optimal codes for this purpose. However, there is a limit to how short the average codeword can be. Specifically, the Source Coding Theorem states that the average information per symbol is always less than or equal to the average length of a codeword: 

$$H ≤ L$$

This inequality is easy to prove using the Gibbs and Kraft inequalities. Use the Gibbs inequality with $p' (A_i) = 1/2^{L_i}$ (the Kraft inequality assures that the $p' (A_i)$, besides being positive, add up to no more than 1).

### 6.4 Channel Model 

A communication channel accepts input bits and produces output bits. We model the input as the selection of one of a finite number of input states (for the simplest channel, two such states), and the output as a similar event. The language of probability theory will be useful in describing channels. If the channel perfectly changes its output state in conformance with its input state, it is said to be noiseless and in that case nothing affects the output except the input. Let us say that the channel has a certain maximum rate W at which its output can follow changes at the input (just as the source has a rate R at which symbols are selected).

For a noiseless channel, where each of n possible input states leads to exactly one output state, each new input state (R per second) can be specified with $log_2 n$ bits. Thus for the binary channel, n = 2, and so the new state can be specified with one bit. The maximum rate at which information supplied to the input can affect the output is called the channel capacity $C = W log_2 n$ bits per second. For the binary channel, C = W. 

If the input is changed at a rate R less than W (or, equivalently, if the information supplied at the input is less than C) then the output can follow the input, and the output events can be used to infer the identity of the input symbols at that rate. If there is an attempt to change the input more rapidly, the channel cannot follow (since W is by definition the maximum rate at which changes at the input affect the output) and some of the input information is lost.

### 6.5 Noiseless Channel Theorem 

If the channel does not introduce any errors, the relation between the information supplied to the input and what is available on the output is very simple. Let the input information rate, in bits per second, be denoted D (for example, D might be the entropy per symbol of a source H expressed in bits per symbol, times the rate of the source R in symbols per second). If D ≤ C then the information available at the output can be as high as D (the information at the input), and if D > C then the information available at the output cannot exceed C and so an amount at least equal to D − C is lost. This result is pictured in Figure 6.4. 

Note that this result places a limit on how fast information can be transmitted across a given channel. It does not indicate how to achieve results close to this limit. However, it is known how to use Huffman codes to efficiently represent streams of symbols by streams of bits. If the channel is a binary channel it is simply a matter of using that stream of bits to change the input. For other channels, with more than two possible input states, operation close to the limit involves using multiple bits to control the input rapidly.

### 6.6 Noisy Channel 

If the channel introduces noise then the output is not a unique function of the input. We will model this case by saying that for every possible input (which are mutually exclusive states indexed by i) there may be more than one possible output outcome.

However, with noise there is some residual uncertainty. We will calculate this uncertainty in terms of the transition probabilities cji and define the information that we have learned about the input as a result of knowing the output as the mutual information. From that we will define the channel capacity C.


### 6.7 Noisy Channel Capacity Theorem 

The channel capacity of a noisy channel is defined in terms of the mutual information M. 

The channel capacity theorem was first proved by Shannon in 1948. It gives a fundamental limit to the rate at which information can be transmitted through a channel. If the input information rate in bits per second D is less than C then it is possible (perhaps by dealing with long sequences of inputs together) to code the data in such a way that the error rate is as low as desired. On the other hand, if D > C then this is not possible; in fact the maximum rate at which information about the input can be inferred from learning the output is C. 

This result is exactly the same as the result for the noiseless channel, shown in Figure 6.4. This result is really quite remarkable. A capacity figure, which depends only on the channel, was defined and then the theorem states that a code which gives performance arbitrarily close to this capacity can be found. In conjunction with the source coding theorem, it implies that a communication channel can be designed in two stages—first, the source is encoded so that the average length of codewords is equal to its entropy, and second, this stream of bits can then be transmitted at any rate up to the channel capacity with arbitrarily low error. The channel capacity is not the same as the native rate at which the input can change, but rather is degraded from that value because of the noise. 

Unfortunately, the proof of this theorem (which is not given here) does not indicate how to go about finding such a code. In other words, it is not a constructive proof, in which the assertion is proved by displaying the code. In the half century since Shannon published this theorem, there have been numerous discoveries of better and better codes, to meet a variety of high speed data communication needs. However, there is not yet any general theory of how to design codes from scratch (such as the Huffman procedure provides for source coding). 

Claude Shannon (1916–2001) is rightly regarded as the greatest figure in communications in all history.2 He established the entire field of scientific inquiry known today as information theory. He did this work while at Bell Laboratories, after he graduated from MIT with his S.M. in electrical engineering and his Ph.D. in mathematics. It was he who recognized the binary digit as the fundamental element in all communications. In 1956 he returned to MIT as a faculty member. In his later life he suffered from Alzheimer’s disease, and, sadly, was unable to attend a symposium held at MIT in 1998 honoring the 50th anniversary of his seminal paper.

### 6.8 Reversibility 

It is instructive to note which operations discussed so far involve loss of information, and which do not. 

Some Boolean operations had the property that the input could not be deduced from the output. The AND and OR gates are examples. Other operations were reversible—the EXOR gate, when the output is augmented by one of the two inputs, is an example. 

Some sources may be encoded so that all possible symbols are represented by different codewords. This is always possible if the number of symbols is finite. Other sources have an infinite number of possible symbols, and these cannot be encoded exactly. Among the techniques used to encode such sources are binary codes for integers (which suffer from overflow problems) and floating-point representation of real numbers (which suffer from overflow and underflow problems and also from limited precision). 

Some compression algorithms are reversible in the sense that the input can be recovered exactly from the output. One such technique is LZW, which is used for text compression and some image compression, among other things. Other algorithms achieve greater efficiency at the expense of some loss of information. Examples are JPEG compression of images and MP3 compression of audio. 

Now we have seen that some communication channels are noiseless, and in that case there can be perfect transmission at rates up to the channel capacity. Other channels have noise, and perfect, reversible communication is not possible, although the error rate can be made arbitrarily small if the data rate is less than the channel capacity. For greater data rates the channel is necessarily irreversible. 

In all these cases of irreversibility, information is lost, (or at best kept unchanged). Never is information increased in any of the systems we have considered. 

Is there a general principle at work here?

### 6.9 Detail: Communication System Requirements 

The model of a communication system that we have been developing is shown in Figure 6.1. The source is assumed to emit a stream of symbols. The channel may be a physical channel between different points in space, or it may be a memory which stores information for retrieval at a later time, or it may even be a computation in which the information is processed in some way. 

Naturally, different communication systems, though they all might be well described by our model, differ in their requirements. The following table is an attempt to illustrate the range of requirements that are reasonable for modern systems. It is, of course, not complete. 

The systems are characterized by four measures: throughput, latency, tolerance of errors, and tolerance to nonuniform rate (bursts). Throughput is simply the number of bits per second that such a system should, to be successful, accommodate. Latency is the time delay of the message; it could be defined either as the delay of the start of the output after the source begins, or a similar quantity about the end of the message (or, for that matter, about any particular features in the message). The numbers for throughput, in MB (megabytes) or kb (kilobits) are approximate.

## Unit 7: Processes

The processes we consider here are 

- Discrete: The inputs are members of a set of mutually exclusive possibilities, only one of which occurs at a time, and the output is one of another discrete set of mutually exclusive events. 
- Finite: The set of possible inputs is finite in number, as is the set of possible outputs. 
- Memoryless: The process acts on the input at some time and produces an output based on that input, ignoring any prior inputs.
- Nondeterministic: The process may produce a different output when presented with the same input a second time (the model is also valid for deterministic processes). Because the process is nondeterministic the output may contain random noise. 
- Lossy: It may not be possible to “see” the input from the output, i.e., determine the input by observing the output. Such processes are called lossy because knowledge about the input is lost when the output is created (the model is also valid for lossless processes).

### 7.1 Types of Process Diagrams

Different diagrams of processes are useful for different purposes. The four we use here are all recursive, meaning that a process may be represented in terms of other, more detailed processes of the same sort, interconnected. Conversely, two or more connected processes may be represented by a single higher-level process with some of the detailed information suppressed. The processes represented can be either deterministic (noiseless) or nondeterministic (noisy), and either lossless or lossy.

- Block Diagram
- Circuit Diagram
- Probability Diagram:
- Information Diagram

### 7.2 Probability Diagrams

Unfortunately, the probability model is awkward when the number of input bits is moderate or large. The reason is that the inputs and outputs are represented in terms of mutually exclusive sets of events. If the events describe signals on, say, five wires, each of which can carry a high or low voltage signifying a boolean 1 or 0, there would be 32 possible events. It is much easier to draw a logic gate, with five inputs representing physical variables, than a probability process with 32 input states. This “exponential explosion” of the number of possible input states gets even more severe when the process represents the evolution of the state of a physical system with a large number of atoms.

This description has great generality. It applies to a deterministic process (although it may not be the most convenient—a truth table giving the output for each of the inputs is usually simpler to think about). For such a process, each column of the $c_{ji}$ matrix contains one element that is 1 and all the other elements are 0. It also applies to a nondeterministic channel (i.e., one with noise). It applies to the source encoder and decoder, to the compressor and expander, and to the channel encoder and decoder. It applies to logic gates and to devices which perform arbitrary memoryless computation (sometimes called “combinational logic” in distinction to “sequential logic” which can involve prior states). It even applies to transitions taken by a physical system from one of its states to the next. It applies if the number of output states is greater than the number of input states (for example channel encoders) or less (for example channel decoders).

### 7.2.1 Example: AND Gate 

The AND gate is deterministic (it has no noise) but is lossy, because knowledge of the output is not generally sufficient to infer the input.

### 7.2.2 Example: Binary Channel 

The binary channel is well described by the probability model. Its properties, many of which were discussed in Chapter 6, are summarized below.

Loss of information happens because it is no longer possible to tell with certainty what the input signal is, when the output is observed. Loss shows up in drawings like Figure 7.6(b) where two or more paths converge on the same output. Noise happens because the output is not determined precisely by the input. Noise shows up in drawings like Figure 7.6(b) where two or more paths diverge from the same input. Despite noise and loss, however, some information can be transmitted from the input to the output (i.e., observation of the output can allow one to make some inferences about the input). 

We now return to our model of a general discrete memoryless nondeterministic lossy process, and derive formulas for noise, loss, and information transfer (which will be called “mutual information”). We will then come back to the symmetric binary channel and interpret these formulas.

### 7.3 Information, Loss, and Noise

Processes with outputs that can be produced by more than one input have loss. These processes may also be nondeterministic, in the sense that one input state can lead to more than one output state. The symmetric binary channel with loss is an example of a process that has loss and is also nondeterministic. However, there are some processes that have loss but are deterministic. An example is the AND logic gate, which has four mutually exclusive inputs 00 01 10 11 and two outputs 0 and 1. Three of the four inputs lead to the output 0. This gate has loss but is perfectly deterministic because each input state leads to exactly one output state. The fact that there is loss means that the AND gate is not reversible.

#### 7.3.1 Example: Symmetric Binary Channel

### 7.4 Deterministic Examples

This probability model applies to any system with mutually exclusive inputs and outputs, whether or not the transitions are random. If all the transition probabilities $c_{ji}$ are equal to either 0 or 1, then the process is deterministic. 

A simple example of a deterministic process is the NOT gate, which implements Boolean negation. If the input is 1 the output is 0 and vice versa. The input and output information are the same, I = J and there is no noise or loss: N = L = 0. The information that gets through the gate is M = I. See Figure 7.7(a). 

A slightly more complex deterministic process is the exclusive or, XOR gate. This is a Boolean function of two input variables and therefore there are four possible input values.

#### 7.4.1 Error Correcting Example 

The Hamming Code encoder and decoder can be represented as discrete processes in this form.

### 7.5 Capacity

Then the process capacity C is defined as $C = WM_{max}$

### 7.6 Information Diagrams 

An information diagram is a representation of one or more processes explicitly showing the amount of information passing among them. It is a useful way of representing the input, output, and mutual information and the noise and loss. Information diagrams are at a high level of abstraction and do not display the detailed probabilities that give rise to these information measures.

Information diagrams are not often used for communication systems. There is usually no need to account for the noise sources or what happens to the lost information. However, such diagrams are useful in domains where noise and loss cannot occur. One example is reversible computing, a style of computation in which the entire process can, in principle, be run backwards. Another example is quantum communications, where information cannot be discarded without affecting the environment.

### 7.6.1 Notation

### 7.7 Cascaded Processes

Consider two processes in cascade. This term refers to having the output from one process serve as the input to another process. Then the two cascaded processes can be modeled as one larger process, if the “internal” states are hidden.

注释：

A cascade process refers to a series of steps or stages in a process where each step is dependent on the previous one. It is commonly used in contexts such as:

- Purification or Enrichment: A cascade process is employed when one stage of enrichment is not sufficient to achieve the desired concentration of a substance. 
- Efficiency: It can also refer to any process that occurs in multiple steps because a single step is too inefficient to produce the desired result. 

These definitions highlight the importance of sequential steps in achieving a specific outcome in various fields.

## Unit 8: Inference

In Chapter 7 the process model was introduced as a way of accounting for flow of information through processes that are discrete, finite, and memoryless, and which may be nondeterministic and lossy. Although the model was motivated by the way many communication systems work, it is more general. 

Formulas were given for input information I, loss L, mutual information M, noise N, and output information J. Each of these is measured in bits, although in a setting in which many symbols are chosen, one after another, they may be multiplied by the rate of symbol selection and then expressed in bits per second. The information flow is shown in Figure 8.1. All these quantities depend on the input probability distribution $p(A_i)$. 

If the input probabilities are already known, and a particular output outcome is observed, it is possible to make inferences about the input event that led to that outcome. Sometimes the input event can be identified with certainty, but more often the inferences are in the form of changes in the initial input probabilities. This is typically how communication systems work—the output is observed and the “most likely” input event is inferred. Inference in this context is sometime referred to as estimation. It is the topic of Section 8.1. 

On the other hand, if the input probabilities are not known, this approach does not work. We need a way to get the initial probability distribution. An approach that is based on the information analysis is discussed in Section 8.2 and in subsequent chapters of these notes. This is the Principle of Maximum Entropy

### 8.1 Estimation 

It is often necessary to determine the input event when only the output event has been observed. This is the case for communication systems, in which the objective is to infer the symbol emitted by the source so that it can be reproduced at the output. It is also the case for memory systems, in which the objective is to recreate the original bit pattern without error.

Two of the following examples will be continued in subsequent chapters including the next chapter on the Principle of Maximum Entropy—the symmetric binary channel and Berger’s Burgers.

#### 8.1.1 Symmetric Binary Channel

#### 8.1.2 Non-symmetric Binary Channel

A non-symmetric binary channel is one in which the error probabilities for inputs 0 and 1 are different, i.e., $c_{01} \neq c_{10}$. We illustrate non-symmetric binary channels with an extreme case based on a medical test for Huntington’s Disease.

#### 8.1.3 Berger’s Burgers

#### 8.1.4 Inference Strategy 

Often, it is not sufficient to calculate the probabilities of the various possible input events. The correct operation of a system may require that a definite choice be made of exactly one input event. For processes without loss, this can be done accurately. However, for processes with loss, some strategy must be used to convert probabilities to a single choice. 

One simple strategy, “maximum likelihood,” is to decide on whichever input event has the highest probability after the output event is known. For many applications, particularly communication with small error, this is a good strategy. It works for the symmetric binary channel when the two input probabilities are equal. However, sometimes it does not work at all. For example, if used for the Huntington’s Disease test on people without a family history, this strategy would never say that the person has a defective gene, regardless of the test results. 

Inference is important in many fields of interest, such as machine learning, natural language processing and other areas of artificial intelligence. An open question, of current research interest, is which inference strategies are best suited for particular purposes.

### 8.2 Principle of Maximum Entropy: Simple Form 

In the last section, we discussed one technique of estimating the input probabilities of a process given that the output event is known. This technique, which relies on the use of Bayes’ Theorem, only works if the process is lossless (in which case the input can be identified with certainty) or an initial input probability distribution is assumed (in which case it is refined to take account of the known output). 

The Principle of Maximum Entropy is a technique that can be used to estimate input probabilities more generally. The result is a probability distribution that is consistent with known constraints expressed in terms of averages, or expected values, of one or more quantities, but is otherwise as unbiased as possible (the word “bias” is used here not in the technical sense of statistics, but the everyday sense of a preference that inhibits impartial judgment). This principle is described first for the simple case of one constraint and three input events, in which case the technique can be carried out analytically. Then it is described more generally in Chapter 9. 

This principle has applications in many domains, but was originally motivated by statistical physics, which attempts to relate macroscopic, measurable properties of physical systems to a description at the atomic or molecular level. It can be used to approach physical systems from the point of view of information theory, because the probability distributions can be derived by avoiding the assumption that the observer has more information than is actually available. Information theory, particularly the definition of information in terms of probability distributions, provides a quantitative measure of ignorance (or uncertainty, or entropy) that can be maximized mathematically to find the probability distribution that best avoids unnecessary assumptions.

#### 8.2.1 Berger’s Burgers

#### 8.2.2 Probabilities

#### 8.2.3 Entropy

In the context of physical systems this uncertainty is known as the entropy. In communication systems the uncertainty regarding which actual message is to be transmitted is also known as the entropy of the source. Note that in general the entropy, because it is expressed in terms of probabilities, depends on the observer. One person may have different knowledge of the system from another, and therefore would calculate a different numerical value for entropy. The Principle of Maximum Entropy is used to discover the probability distribution which leads to the highest value for this uncertainty, thereby assuring that no information is inadvertently assumed. The resulting probability distribution is not observer-dependent.

#### 8.2.4 Constraints 

It is a property of the entropy formula above that it has its maximum value when all probabilities are equal (we assume the number of possible states is finite). This property is easily proved using the Gibbs inequality. If we have no additional information about the system, then such a result seems reasonable. However, if we have additional information then we ought to be able to find a probability distribution that is better in the sense that it has less uncertainty.

#### 8.2.5 Maximum Entropy, Analytic Form

The Principle of Maximum Entropy is based on the reasonable assumption that you should select that probability distribution which leaves you the largest remaining uncertainty (i.e., the maximum entropy) consistent with your constraints. That way you have not introduced any additional assumptions into your calculations.

#### 8.2.6 Summary 

Let’s remind ourselves what we have done. We have expressed our constraints in terms of the unknown probability distributions. One of these constraints is that the sum of the probabilities is 1. The other involves the average value of some quantity, in this case cost. We used these constraints to eliminate two of the variables. We then expressed the entropy in terms of the remaining variable. Finally, we found the value of the remaining variable for which the entropy is the largest. The result is a probability distribution that is consistent with the constraints but which has the largest possible uncertainty. Thus we have not inadvertently introduced any unwanted assumptions into the probability estimation. 

This technique requires that the model for the system be known at the outset; the only thing not known is the probability distribution. As carried out in this section, with a small number of unknowns and one more unknown than constraint, the derivation can be done analytically. For more complex situations a more general approach is necessary. That is the topic of Chapter 9.

## Unit 9: Maximum Entropy

Section 8.2 presented the technique of estimating input probabilities of a process that are unbiased but consistent with known constraints expressed in terms of averages, or expected values, of one or more quantities. This technique, the Principle of Maximum Entropy, was developed there for the simple case of one constraint and three input events, in which case the technique can be carried out analytically. It is described here for the more general case. 

### 9.1 Problem Setup

#### 9.1.1 Berger’s Burgers

#### 9.1.2 Magnetic Dipole Model

### 9.2 Probabilities

### 9.3 Entropy

Our uncertainty is expressed quantitatively by the information which we do not have about the state occupied.

![](https://setsailtowardstianhan.ip-ddns.com/blog/3edebee0526a7457c913dae5fc0b465f.png)

### 9.4 Constraints

The entropy has its maximum value when all probabilities are equal (we assume the number of possible states is finite), and the resulting value for entropy is the logarithm of the number of states, with a possible scale factor like $k_B$. If we have no additional information about the system, then such a result seems reasonable. However, if we have additional information in the form of constraints then the assumption of equal probabilities would probably not be consistent with those constraints. Our objective is to find the probability distribution that has the greatest uncertainty, and hence is as unbiased as possible.

#### 9.4.1 Examples

### 9.5 Maximum Entropy, Analytic Form 

The Principle of Maximum Entropy is based on the premise that when estimating the probability distribution, you should select that distribution which leaves you the largest remaining uncertainty (i.e., the maximum entropy) consistent with your constraints. That way you have not introduced any additional assumptions or biases into your calculations.

### 9.6 Maximum Entropy, Single Constraint

![](https://setsailtowardstianhan.ip-ddns.com/blog/d7b04be9c9213bed3b1b5f208402351a.png)

#### 9.6.1 Dual Variable

Lagrange Multiplier

#### 9.6.2 Probability Formula

The function α(β) is related to the partition function Z(β) of statistical physics: $Z = 2α$ or $α = log_2 Z$.

#### 9.6.3 The Maximum Entropy



#### 9.6.4 Evaluating the Dual Variable




#### 9.6.5 Examples

![](https://setsailtowardstianhan.ip-ddns.com/blog/1464e6f332b1b5468848a24ebdd0d5d0.png)

## Unit 10: Physical Systems

The model of information separated from its physical embodiment is, of course, an approximation of reality. Eventually, as we make microelectronic systems more and more complicated, using smaller and smaller components, we will need to face the fundamental limits imposed not by our ability to fabricate small structures, but by the laws of physics. All physical systems are governed by quantum mechanics. 

Quantum mechanics is often believed to be of importance only for small structures, say the size of an atom. Although it is unavoidable at that length scale, it also governs everyday objects. When dealing with information processing in physical systems, it is pertinent to consider both very small systems with a small number of bits of information, and large systems with large amounts of information. 

The key ideas we have used thus far that need to be re-interpreted in the regime where quantum mechanics is important include

- The digital abstraction made practical by devices that can restore data with small perturbations 
- Use of probability to express our knowledge in the face of uncertainty 
- The Principle of Maximum Entropy as a technique to estimate probabilities without bias

### 10.1 Nature of Quantum Mechanics

In light of these disadvantages, why is quantum mechanics important? Because it works. It is the ONLY fundamental physical theory that works over such a wide range of situations. Its predictions have been verified experimentally time after time. It applies to everyday size objects, and to astronomical objects (although it is usually not necessary for them). It applies to atomic-size objects, to electromagnetic waves, and to sub-atomic objects. There is a version that is compatible with the theory of special relativity. About the only physical phenomenon not handled well at this time is gravity; quantum mechanics has not yet been extended to be compatible with the theory of general relativity.

In these notes we cannot cover quantum mechanics in much depth. For the purpose of examining information processing in physical systems, we only need to understand a few of the general features such systems must have. In particular, we need a model of physical systems in which there are many possible states, each with its own probability of being the one the system is actually in (i.e., the state “occupied”). These states all have physical properties associated with them, and energy is one of these. Quantum mechanics justifies this model. 

We will use this model in two situations. The first (below) is one with many states, where the objective is to understand how the information associated with the occupancy of these states affects the flow of energy. The second (in a later chapter of these notes) is one with a very small number of states, where information is represented using the occupancy of these states, and the objective is to understand both the limits and opportunities in information processing afforded by quantum mechanics. 

The next two sections, Section 10.2 “Introduction to Quantum Mechanics” and Section 10.3 “Stationary States,” may be skipped by readers who are prepared to accept the state model without justification. They may proceed directly to Section 10.4 “Multi-State Model.” Other readers may glean from the next two sections some indication of how quantum considerations lead to that model, and in the process may find some aspects of quantum mechanics less mysterious.

### 10.2 Introduction to Quantum Mechanics

### 10.3 Stationary States

### 10.4 Multi-State Model

#### 10.4.1 Energy Systems

This model is set up in a way that is perfectly suited for the use of the Principle of Maximum Entropy to estimate the occupation probability distribution $p_j$ . This topic will be pursued in Chapter 11 of these notes.

#### 10.4.2 Information Systems

An object intended to perform information storage, transmission, or processing should avoid the errors that are inherent in unpredictable interactions with the environment. It would seem that the simplest such object that could process information would need two states. One bit of information could be associated with the knowledge of which state is occupied. More complex objects, with more than two states, could represent more than one bit of information. 

Quantum information systems, including computers and communication systems, will be the topic of Chapter 13 of these notes.

## Unit 11: Energy

In Chapter 9 of these notes we introduced the Principle of Maximum Entropy as a technique for estimating probability distributions consistent with constraints. 

A simple case that can be done analytically is that in which there are three probabilities, one constraint in the form of an average value, and the fact that the probabilities add up to one. There are, then, two equations in three unknowns, and it is straightforward to express the entropy in terms of one of the unknowns, eliminate the others, and find the maximum. This approach also works if there are four probabilities and two average-value constraints, in which case there is again one fewer equation than unknown. 

Another special case is one in which there are many probabilities but only one average constraint. Although the entropy cannot be expressed in terms of a single probability, the solution in Chapter 9 is practical if the summations can be calculated. 

In the application of the Principle of Maximum Entropy to physical systems, the number of possible states is usually very large, so that neither analytic nor numerical solutions are practical. Even in this case, however, the Principle of Maximum Entropy is useful because it leads to relationships among different quantities. In this chapter we look at general features of such systems. 

Because we are now interested in physical systems, we will express entropy in Joules per Kelvin rather than in bits, and use the natural logarithm rather than the logarithm to the base 2.

### 11.1 Magnetic Dipole Model

### 11.2 Principle of Maximum Entropy for Physical Systems

#### 11.2.1 General Properties

#### 11.2.2 Differential Forms

#### 11.2.3 Differential Forms with External Parameters

### 11.3 System and Environment 

The formulas to this point apply to the system if the summations are over the states of the system, and they also apply to the system and its environment if the summations are over the larger number of states of the system and environment together. (The magnetic-dipole model of Figure 11.1 even shows a system capable of interacting with either of two environments, a feature that is needed if the system is used for energy conversion.) Next are some results for a system and its environment interacting. 

#### 11.3.1 Partition Model 

Let us model the system and its environment (for the moment consider only one such environment) as parts of the universe that each have their own set of possible states, and which can be isolated from each other or can be in contact. That is, the system, considered apart from its environment, has states which, at least in principle, can be described. Each has an energy associated with it, and perhaps other physical properties as well. This description is separate from the determination of which state is actually occupied—that determination is made using the Principle of Maximum Entropy.

#### 11.3.2 Interaction Model 

The reason for our partition model is that we want to control interaction between the system and its environment. Different physical systems would have different modes of interaction, and different mechanisms for isolating different parts. Here is described a simple model for interaction of magnetic dipoles that are aligned in a row. It is offered as an example.

#### 11.3.3 Extensive and Intensive Quantities 

This partition model leads to an important property that physical quantities can have. Some physical quantities will be called “extensive” and others “intensive.”

#### 11.3.4 Equilibrium

The partition model leads to interesting results when the system and its environment are allowed to come into contact after having been isolated. In thermodynamics this process is known as the total configuration coming into equilibrium.
#### 11.3.5 Energy Flow, Work and Heat

Changes to a system caused by a change in one or more of its parameters, when it cannot interact with its environment, are known as adiabatic changes. Since the probability distribution is not changed by them, they produce no change in entropy of the system. This is a general principle: adiabatic changes do not change the probability distribution and therefore conserve entropy.
#### 11.3.6 Reversible Energy Flow

We saw in section 11.3.4 that when a system is allowed to interact with its environment, total entropy generally increases. In this case it is not possible to restore the system and the environment to their prior states by further mixing, because such a restoration would require a lower total entropy. Thus mixing in general is irreversible. 

The limiting case where the total entropy stays constant is one where, if the system has changed, it can be restored to its prior state. It is easy to derive the conditions under which such changes are, in this sense, reversible.

## Unit 12: Temperature

In previous chapters of these notes we introduced the Principle of Maximum Entropy as a technique for estimating probability distributions consistent with constraints. 

In Chapter 8 we discussed the simple case that can be done analytically, in which there are three probabilities, one constraint in the form of an average value, and the fact that the probabilities add up to one. There are, then, two equations and three unknowns, and it is straightforward to express the entropy in terms of one of the unknowns, eliminating the others, and find the maximum. This approach also works if there are four probabilities and two average-value constraints, in which case there is again one fewer equation than unknown. 

In Chapter 9 we discussed a general case in which there are many probabilities but only one average constraint, so that the entropy cannot be expressed in terms of a single probability. The result previously derived using the method of Lagrange multipliers was given. 

In Chapter 11 we looked at the implications of the Principle of Maximum Entropy for physical systems that adhere to the multi-state model motivated by quantum mechanics, as outlined in Chapter 10. 

We found that the dual variable β plays a central role. Its value indicates whether states with high or low energy are occupied (or have a higher probability of being occupied). From it all the other quantities, including the expected value of energy and the entropy, can be calculated.

In this chapter, we will interpret β further, and will define its reciprocal as (to within a scale factor) the temperature of the material. Then we will see that there are constraints on the efficiency of energy conversion that can be expressed naturally in terms of temperature.

### 12.1 Temperature Scales

Absolute temperature T is measured in Kelvins (sometimes incorrectly called degrees Kelvin), in honor of William Thomson (1824–1907), who proposed an absolute temperature scale in 1848.1 The Celsius scale, which is commonly used by the general public in most countries of the world, differs from the Kelvin scale by an additive constant, and the Fahrenheit scale, which is in common use in the United States, differs by both an additive constant and a multiplicative factor. Finally, to complete the roster of scales, William Rankine (1820–1872) proposed a scale which had 0 the same as the Kelvin scale, but the size of the degrees was the same as in the Fahrenheit scale. 

More than one temperature scale is needed because temperature is used for both scientific purposes (for which the Kelvin scale is well suited) and everyday experience. Naturally, the early scales were designed for use by the general public. Gabriel Fahrenheit (1686–1736) wanted a scale where the hottest and coldest weather in Europe would lie between 0 and 100. He realized that most people can deal most easily with numbers in that range. In 1742 Anders Celsius (1701–1744) decided that temperatures between 0 and 100 should cover the range where water is a liquid. In his initial Centigrade Scale, he represented the boiling point of water as 0 degrees and the freezing point as 100 degrees. Two years later it was suggested that these points be reversed.2 The result, named after Celsius in 1948, is now used throughout the world.

Comments:

1. Thomson was a prolific scientist/engineer at Glasgow University in Scotland, with major contributions to electromagnetism, thermodynamics, and their industrial applications. He invented the name “Maxwell’s Demon.” In 1892 he was created Baron Kelvin of Largs for his work on the transatlantic cable. Kelvin is the name of the river that flows through the University. 
2. According to some accounts the suggestion was made by Carolus Linnaeus (1707–1778), a colleague on the faculty of Uppsala University and a protege of Celsius’ uncle. Linnaeus is best known as the inventor of the scientific notation for plants and animals that is used to this day by botanists and zoologists.

### 12.2 Heat Engine

The magnetic-dipole system we are considering is shown in Figure 12.1, where there are two environments at different temperatures, and the interaction of each with the system can be controlled by having the barriers either present or not (shown in the Figure as present). Although Figure 12.1 shows two dipoles in the system, the analysis here works with only one dipole, or with more than two, so long as there are many fewer dipoles in the system than in either environment.

### 12.3 Energy-Conversion Cycle

This ratio is known as the Carnot efficiency, named after the French physicist Sadi Nicolas L´eonard Carnot (1796 - 1832).3 He was the first to recognize that heat engines could not have perfect efficiency, and that the efficiency limit (which was subsequently named after him) applies to all types of reversible heat engines.
## Unit 13: Quantum Information

In Chapter 10 of these notes the multi-state model for quantum systems was presented. This model was then applied to systems intended for energy conversion in Chapter 11 and Chapter 12. Now it is applied to systems intended for information processing. 

The science and technology of quantum information is relatively new. The concept of the quantum bit (named the qubit) was first presented, in the form needed here, in 1995. There are still many unanswered questions about quantum information (for example the quantum version of the channel capacity theorem is not known precisely). As a result, the field is in a state of flux. There are gaps in our knowledge.

### 13.1 Quantum Information Storage

We have used the bit as the mathematical model of the simplest classical system that can store information. Similarly, we need a model for the simplest quantum system that can store information. It is called the “qubit.” At its simplest, a qubit can be thought of as a small physical object with two states, which can be placed in one of those states and which can subsequently be accessed by a measurement instrument that will reveal that state. However, quantum mechanics both restricts the types of interactions that can be used to move information to or from the system, and permits additional modes of information storage and processing that have no classical counterparts. 

An example of a qubit is the magnetic dipole which was used in Chapters 9, 11, and 12 of these notes. Other examples of potential technological importance are quantum dots (three-dimensional wells for trapping electrons) and photons (particles of light with various polarizations). 

Qubits are difficult to deal with physically. That’s why quantum computers are not yet available. While it may not be hard to create qubits, it is often hard to measure them, and usually very hard to keep them from interacting with the rest of the universe and thereby changing their state unpredictably.

However, there are at least three reasons why we may want to store bits without such massive redundancy. First, it would be more efficient. More bits could be stored or processed in a structure of the same size or cost. The semiconductor industry is making rapid progress in this direction, and before 2015 it should be possible to make memory cells and gates that use so few atoms that statistical fluctuations in the number of data-storing particles will be a problem. Second, sensitive information stored without redundancy could not be copied without altering it, so it would be possible to protect the information securely, or at least know if its security had been compromised. And third, the properties of quantum mechanics could permit modes of computing and communications that cannot be done classically. 

A model for reading and writing the quantum bit is needed. Our model for writing (sometimes called “preparing” the bit) is that a “probe” with known state (either “up” or “down”) is brought into contact with the single dipole of the system. The system and the probe then exchange their states. The system ends up with the probe’s previous value, and the probe ends up with the system’s previous value. If the previous system state was known, then the state of the probe after writing is known and the probe can be used again. If not, then the probe cannot be reused because of uncertainty about its state. Thus writing to a system that has unknown data increases the uncertainty about the environment. The general principle here is that discarding unknown data increases entropy. 

The model for reading the quantum bit is not as simple. We assume that the measuring instrument interacts with the bit in some way to determine its state. This interaction forces the system into one of its stationary states, and the state of the instrument changes in a way determined by which state the system ends up in. If the system was already in one of the stationary states, then that one is the one selected. If, more generally, the system wave function is a linear combination of stationary states, then one of those states is selected, with probability given by the square of the magnitude of the expansion coefficient. 

We now present three models of quantum bits, with increasingly complicated behavior.

### 13.2 Model 1: Tiny Classical Bits

### 13.3 Model 2: Superposition of States (the Qubit)

### 13.4 Model 3: Multiple Qubits with Entanglement

It is possible to define several interesting logic gates which act on multiple qubits. These have the property that they are reversible; this is a general property of quantum-mechanical systems.

Among the interesting applications of multiple qubits are 

- Computing some algorithms (including factoring integers) faster than classical computers 
- Teleportation (of the information needed to reconstruct a quantum state) 
- Cryptographic systems • Backwards information transfer (not possible classically) 
- Superdense coding (two classical bits in one qubit if another qubit was sent earlier)

### 13.5 Detail: Qubit and Applications

To emphasize that we are interested in the dynamics of two-state systems, and not in the dynamics of each state, it is best to abstract the wave function and introduce a new notation, the bracket notation. In the following sections, as we introduce the bracket notation, we appreciate the first important differences with the classical domain: the no-cloning theorem and entanglement. Then we give an overview of the applications of quantum mechanics to communication (teleportation and cryptography), algorithms (Grover fast search, Deutsch-Josza) and information science (error correcting codes).

### 13.6 Bracket Notation for Qubits

The bracket notation was introduced by P. Dirac for quantum mechanics. In the context of these notes, bracket notation will give us a new way to represent old friends like column and row vectors, dot products, matrices, and linear transformations. Nevertheless, bracket notation is more general than that; it can be used to fully describe wave functions with continuous variables such as position or momentum.

#### 13.6.1 Kets, Bras, Brackets, and Operators

Kets, bras, brackets and operators are the building bricks of bracket notation, which is the most commonly used notation for quantum mechanical systems. They can be thought of as column vectors, row vectors, dot products and matrices respectively.

Bras are the Hermitian conjugates of kets. That is, for a given ket, the corresponding bra is a row vector (the transpose of a ket), where the elements have been complex conjugated.

![](https://setsailtowardstianhan.ip-ddns.com/blog/d8b904b628fdcc3e2767cc594ecac0ac.png)

![](https://setsailtowardstianhan.ip-ddns.com/blog/d10f5bddfeeb791fcfea73381003efba.png)

#### 13.6.2 Tensor Product—Composite Systems

The notation we have introduced so far deals with single qubit systems. It is nonetheless desirable to have a notation that allows us to describe composite systems, that is systems of multiple qubits. A similar situation arises in set theory when we have two sets A and B and we want to consider them as a whole. In set theory to form the ensemble set we use the cartesian product A×B to represent the ensemble of the two sets. The analogue in linear algebra is called tensor product and is represented by the symbol ⊗. It applies equally to vectors and matrices (i.e. kets and operators).

![](https://setsailtowardstianhan.ip-ddns.com/blog/5465bd4b372d144dae8569bfb2a3dbbf.png)

You should take some time to get used to the tensor product, and ensure you do not get confused with all the different products we have introduced in in the last two sections.

![](https://setsailtowardstianhan.ip-ddns.com/blog/c3f6805c00b2d7d5a7898a73a8018243.png)

#### 13.6.3 Entangled qubits

We have previously introduced the notion of entanglement in terms of wave functions of a system that allows two measurements to be made. Here we see that it follows from the properties of the tensor product a as a means to concatenate systems.

The most salient difference with what we saw in the mixing process arises from the fact that, as Schrodinger points out in the paragraph above, this “interleaving” of the parts remains even after separating them, and the measurement of one of the parts will condition the result on the other. This is what Einstein called “spooky action at a distance”.

### 13.7 No Cloning Theorem

One of the most natural operations in classical information is to copy bits, it happens all the time in our computers. Quantum logic diverges from classical logic already at this level. Qubits cannot be copied, or as it is usually stated: qubits cannot be cloned.

There are several intuitive arguments that can help us understand why it is so. Remember that in Chapter 10 we emphasized that the act of measuring changes the system being measured; if the system is in a superposition, the result of the measurement will be one of the states of the superposition. And the superposition is destroyed. Intuitively, if measuring is at all required to do the cloning, then it will be impossible to have two clones, since we cannot learn anything about the initial superposition. Furthermore, the superposition itself is destroyed by the act of measuring. This implies that a viable cloning device cannot use measurement.

### 13.8 Representation of Qubits 

The no-cloning theorem prepares us to expect changes in quantum logic with respect to its classical analog. To fully appreciate the differences, we have to work out a representation of the qubit that unlike the classical bit, allows us to picture superpositions. We will introduce two such representations, a pictorial one that represents the qubit bit as a point in the surface of a sphere, and an operational one that presents the qubit as a line in a circuit much like the logic circuits we explored in Chapter 1.

#### 13.8.1 Qubits in the Bloch sphere

We see that the global phase factor squares to one, and so plays no role in the calculation of the probability. It is often argued that global phase factors disappear when computing probabilities, and so, are not measurable. 

#### 13.8.2 Qubits and symmetries 

The Bloch sphere depicts each operation on a qubit as a trajectory on the sphere. However, any trajectory on the sphere can be represented by means of a sequence of rotations about the three axis. So, one way to address the definition of the operations on the qubit is to study rotations about the axis of the bloch sphere. This is intimately connected with the study of symmetries. Thomas Bohr was the first to suggest to use symmetries to interpret quantum mechanics.

#### 13.8.3 Quantum Gates 

In the first chapter of these notes, we explored all the possible functions of one and two input arguments and then singled out the most useful boolean functions NOT, AND, NAND, NOR, OR, XOR. Then, we associated it to a pictogram that we called gate, and reviewed the mechanisms to build logic circuits to do computations. 

In the previous section we did the same thing for qubits, we characterized all the operators that may transform the value of a single qubit: we defined Pauli’s matrices and explained how to do arbitrary rotations. By analogy with the classical case, Pauli matrices and arbitrary rotations are the gates of a quantum circuit. In more advanced treatises on quantum computing you would want to prove a variety of results about the quantum gates, such as the minimum set of gates necessary to do any quantum computation and various results on the generalization from 1 to n qubits. Here we will limit ourselves to summarizing the main details of the quantum algebra, its symbolic representation, and its properties.

![](https://setsailtowardstianhan.ip-ddns.com/blog/630e294e1c8bd90c868a5d7a07d8126b.png)

### 13.9 Quantum Communication 

Two of the most tantalizing applications of quantum mechanics applied to information theory come from the field of communications. The first is the possibility that a quantum computer could break classical cryptographic codes in virtually no time. The second is the idea that quantum bits can be teleported. 

In this section we will review the principles behind both teleportation and quantum cryptography (the solution to the problem of code breaking). As we are about to see, entanglement is key in both applications. The two most famous characters in communications: Alice and Bob, will play the main role in teleportation. For quantum cryptography, Eve will play a supporting role. 

#### 13.9.1 Teleportation - Alice and Bob’s story

#### 13.9.2 Quantum Cryptography 

This section is still under construction. Sorry. 

### 13.10 Quantum Algorithms 

This section is still under construction. Sorry. 

#### 13.10.1 Deutsch Josza 

This section is still under construction. Sorry. 

#### 13.10.2 Grover 

This section is still under construction. Sorry. 

### 13.11 Quantum Information Science 

This section is still under construction. Sorry























