---
layout: post
title:  "CryptoZombies.io - Making the Zombie Factory"
description: CryptoZombies is a Free, Open Source, interactive code school that teaches you to build games on Ethereum.
tags: Blockchain SmartContract CryptoZombies
---

## Preface

本系列文章记录了基于 Solidity 区块链编程语言的 CryptoZombies 平台的通关指南;   

## 0x01

第一节直接在右侧调整一下数值，然后点击右下角 `NEXT` 进入下一关即可;   

![](https://aloneposix.github.io/assets/images/Blockchain/01.png)

## 0x02

按照题目要求声明编译器版本号为 ^0.4.19，创建一个名为 `ZombieFactory` 的空合约，点击“交卷”;   

![](https://aloneposix.github.io/assets/images/Blockchain/02.png)

## 0x03

uint 是无符号整数变量，无符号整型对比有符号整型区别就是无符号整型其值不能为负数，uint 是 uint256 的简写，在 `ZombieFactory` 合约内定义一个名为 `dnaDigits` 的 uint 类型的状态变量，其值为 16;   

![](https://aloneposix.github.io/assets/images/Blockchain/03.png)

## 0x04

Solidity 的数学运算符和其它主流编程语言非常相似，它还支持乘方操作，使用 `**` 表示，这道题目只需要在合约内定义一个名为 `dnaModulus` 的 uint 类型的变量即可，其值为 `10` 的 `dnaModulus` 次方;   

![](https://aloneposix.github.io/assets/images/Blockchain/04.png)

## 0x05

结构体是一个用于处理复杂数据属性集合的数据类型，在合约内定义一个名为 Zombie 的结构体，赋予其两个属性，分别是 string 类型的 `name` 以及 uint 类型的 `dna` 属性;   

![](https://aloneposix.github.io/assets/images/Blockchain/05.png)

## 0x06

数组这一数据类型可以用于存储元素集合，动态数组和静态数组的区别在于是否固定长度，如果没有固定长度则为动态数组，可以动态添加元素，定义一个名为 `zombies` 数据结构为 `Zombie` 的结构体数组，并使用 `public` 对其修饰，表示可公开交互;   

![](https://aloneposix.github.io/assets/images/Blockchain/06.png)

## 0x07

`function` 关键词用于定义 函数/方法，可以在 ( ) 内定义函数接收参数，说白了就是定义函数形参，函数内的定义函数最好使用 `_` 下划线开头，这是个好习惯，在合约内定义一个名为 `createZombie` 的方法，它接收两个参数，分别是 string 类型的 `_name` 参数和 uint 类型的 `_dna` 参数;   

![](https://aloneposix.github.io/assets/images/Blockchain/07.png)

## 0x08

`.push` 关键词用于向数组尾部添加元素，这道题很好理解，`Zombie` 为数据类型，`zombies` 为数组名，使用 `.push` 将传递到 `createZombie` 方法的两个参数经过 `Zombie `结构体处理后添加到 `zombies` 数组中;   

![](https://aloneposix.github.io/assets/images/Blockchain/08.png)

## 0x09

Solidity 定义的函数如果不指定函数属性则默认为 `public`，这意味着任何账户，包括外部账户以及合约账户均可调用合约内的此函数，将函数定义为 `private` 是一个好习惯，只有函数需要被外部调用时才将其设置为 `public` 类型，这符合最小权限原则，定义私有函数需要使用 `private` 对指定函数进行修饰，且私有函数需要以 `_` 开头;   

![](https://aloneposix.github.io/assets/images/Blockchain/09.png)

## 0x10

函数定义时可包含返回的数据类型，`view` 修饰符可以将函数定义为只能读取数据不能修改数据的函数，`pure` 修饰符与其类似，区别在于 `pure` 甚至都不会访问合约内的数据，返回值完全取决于传递的参数，定义一个名为 `_generateRandomDna` 的私有函数，函数接收一个名为`_str` 类型 为 `string` 的参数，由于此函数不需要修改函数内的数据，所以将其标记为 `view`;   

![](https://aloneposix.github.io/assets/images/Blockchain/10.png)

## 0x11

`keccak256` 是 Ethereum 内部定义的散列函数，底层技术为 `SHA3`，散列函数的作用就是将字符串转换为 `256` 位 的 16 进制的数值，当两个不同数据类型的变量进行数学运算时需要对其中一个变量进行强制类型转换，编写 `_generateRandomDna` 函数体，定义一个名为 `rand` 的 uint 类型的变量，其值为经过 `keccak256` 函数处理过后的 `_str` 参数并进行 `uint` 强制类型转换后的值，`_generateRandomDna` 函数返回值为 `rand % dnaModulus`;   

![](https://aloneposix.github.io/assets/images/Blockchain/11.png)

## 0x12

构造一个名为 `createRandomZombie` 的公共函数，定义一个名为 `_name` 的 `string` 类型的形参，函数使用 `public` 修饰为公共函数，函数体内调用 `_generateRandomDna` 函数并传递 `_name` 参数，并将返回值赋值给定义的名为 `randDna` ，类型为 uint 的变量，在 `createRandomZombie` 函数体内调用 `_createZombie`，并传入 `_name` 和 `randDna` 两个参数;   

![](https://aloneposix.github.io/assets/images/Blockchain/12.png)

## 0x13

事件 (`Event`) 是智能合约与区块链进行通讯的一种机制，前端应用可以 `监听` 某些事件并作出反应，`event` 关键词用于定义事件，低版本 `Solidity` 触发事件类似于调用函数，直接调用事件名称即可，高版本 `Solidity` 触发事件需要使用 `emit` 关键词，在合约内函数外定义一个名为 `NewZombie` 的事件，它具备三个形参，`zombieId` (uint) `name` (string) `dna` (uint)，修改 `_createZombie` 函数使得每创建新僵尸加入 `zombies` 数组后触发一次 `NewZombie` 事件，触发 `NewZombie` 事件需要传递一个 `id` 参数，由于数组元素索引从 `0` 开始，所以 `zombies.push() -1 ` 将用于 `id` 参数，此处需留意对 `id` 进行了强制类型转换，`id` 参数定义后即可与 `_name` 以及 `_dna` 传入 `NewZombie` 并触发事件;   

![](https://aloneposix.github.io/assets/images/Blockchain/13.png)


## :)
