---
layout: post
title: Quantum Key Distribution
categories: [technology, qkd]
tags: [quantum key distribution]
description: Short explanation of how quantum key distribution works and security concerns related to it
---

*Note: This blog post is composed purely out of interest and doesn't hold any scientific value whatsoever. Please let me know via e-mail or any of the social media accounts you see on the left menu if you see any information that is misleading or completely wrong.*

### Introduction

In order to understand what QKD is and why it might revolutionize the way we share cryptographic keys, let's first have a look at the traditional cryptographic key distribution systems. In symmetric key cryptography, both the sender and the receiver must exchange keys beforehand and utilize those keys to encrypt/decrypt messages, while in public key cryptography, there are two types of keys generated: public and private. Although public keys can be distributed freely and without compromising security, private keys must be kept secret. If anyone wants to send an encrypted message, they can use the recipient's public key to encrypt the message, which then can only be decrypted using his private key. The security of public key cryptography depends on the irreversibility and complexity of certain mathematical problems, known as one-way functions such as integer factorization, meaning that it is dependent on computational power. With the emergence of quantum computers, this became an issue as studies have shown 2048-bit RSA encryption could be broken in about 8 hours¹. Fortunately, with great computing power comes greater cryptographic key generation and distribution algorithms.

### What is Quantum Key Distribution?

Quantum Key Distribution (QKD) is a method used for secure communication that involves individual light quanta in quantum superposition states. The key idea here is that any third-party involvement will introduce a disturbance to the quantum states that the information is traveling in. Also, the ‘no cloning’ theorem will make it impossible to copy the quantum states for later analysis. In other words, quantum key distribution is assumed to be secure by nature, unlike public key cryptography being dependent on the lack of computational power to break.

QKD takes advantage of two main principles in quantum theory: Heisenberg Uncertainty Principle and quantum entanglement. Based on these principles, many protocols have been suggested for securely exchanging cryptographic keys. The most famous and the first one is developed by Charles H. Bennett and Gilles Brassard in 1984 (BB84) using the Heisenberg Uncertainty Principle, meanwhile Artur Ekert has drawn up E91 (Ekert, 1991) involving quantum entanglement feature².

### Security Concerns

There are a lot of skepticism going on about whether or not the QKD is actually secure by the laws of physics. The argument usually is that QKD involves many ‘secret actions’ that are assumed to be taken by the users, which none of the protocols mention. From a paper titled ‘Is the security of quantum cryptography guaranteed by the laws of physics?’³, Daniel J. Bernstein states that “the laws of physics pose serious obstacles to the security of QKD and the same laws are ignored in all QKD ‘security proofs’”. In section 4 of the same paper, he demonstrates a concrete attack against QKD involving an attacker with enough means to afford a state-of-the-art QKD device and a large array of radio receivers, cameras, microphones etc. allowing him to record gigabytes of data per second. Using the data, the attacker can then compute the most likely possibilities of QKD secrets shared between parties. This is, of course, not an easy task for an attacker and this attack must begin before the victims use QKD as mentioned by Bernstein. However, it is theoretically possible and therefore, he claims to disprove that the QKD is secure by nature⁴.

Other types of conventional and non-conventional attacks are possible against different QKD protocols. Not all of them can be described here in detail but references and resources that are at the end of this post can be used by anyone interested.

### References

* [How a quantum computer could break 2048-bit RSA encryption in 8 hours] (https://www.technologyreview.com/s/613596/how-a-quantum-computer-could-break-2048-bit-rsa-encryption-in-8-hours/)
* [Quantum Information and Computation, Jeffrey Bub, in Philosophy of Physics, 2007] (https://www.elsevier.com/books/philosophy-of-physics/butterfield/978-0-444-51560-5)
* [Is the security of quantum cryptography guaranteed by the laws of physics?] (https://arxiv.org/pdf/1803.04520.pdf)
* [What is Quantum Key Distribution?] (https://www.quintessencelabs.com/wp-content/uploads/2015/08/CSA-What-is-Quantum-Key-Distribution-QKD-1.pdf)

### Other Resources

* [Homodyne-detector-blinding attack in continuous-variable quantum key distribution] (https://arxiv.org/pdf/1805.01620.pdf)
* [High speed coherent one-way quantum key distribution prototype] (https://arxiv.org/pdf/0809.5264.pdf)
* [Quantum key distribution] (https://quantiki.org/wiki/quantum-key-distribution)
