# Go与设计模式


设计模式

<!--more-->

## 单一职责原则

类的职责单一，对外只提供一种功能， 而引起类变化的原因都应该只有一个<br>

如果一个类的承担了太多的职责，那么当一个职责发生变化时，可能会影响到这个类实现其他职责的能力，并且当客户端需要该对象的某一个职责的时候，不得不将其他不需要的职责也全都包含进来，造成代码的冗余。

```go
package main

import (
	"fmt"
)

type ClothesShop struct {
}

func (cs *ClothesShop) Style() {
	fmt.Println("逛街的装扮")
}

type ClothesWork struct {
}

func (cs *ClothesWork) Style() {
	fmt.Println("工作的装扮")
}

func main() {
	// 工作的业务
	cw := ClothesWork{}
	cw.Style()

	// 逛街的业务
	cs := ClothesShop{}
	cs.Style()
}
```

每个类的职责尽量设置为单一，对外只提供一种功能.



## 开闭原则

类的改动通过增加代码进行，而不是修改源代码

```go
package main

import "fmt"

// 抽象的业务员
type AbstractBanker interface {
	DoBusi() // 抽象处理业务接口
}

// 存款的业务员
type SaveBanker struct {
}

func (sb *SaveBanker) DoBusi() {
	fmt.Println("进行了存款")
}

// 转账的业务员
type TransferBanker struct {
}

func (sb *TransferBanker) DoBusi() {
	fmt.Println("进行了转账")
}

// 取钱的业务员
type WithdrawBanker struct {
}

func (wb *WithdrawBanker) DoBusi() {
	fmt.Println("进行了取款")
}

// 实现一个架构层(基于抽象层进行业务封装--针对interface接口进行封装)
func BankBusiness(banker AbstractBanker) {
	// 通过接口向下调用
	banker.DoBusi()
}

func main() {
	/*
		// 存款业务
		sb := SaveBanker{}
		sb.DoBusi()

		// 转账业务
		tb := TransferBanker{}
		tb.DoBusi()

		// 取钱业务
		wb := WithdrawBanker{}
		wb.DoBusi()
	*/

	// 存款业务
	BankBusiness(&SaveBanker{})
	// 转账业务
	BankBusiness(&TransferBanker{})
	// 取钱业务
	BankBusiness(&WithdrawBanker{})

}
```

将银行业务员的职责按照业务分开，后续在有新的业务时，可以通过增加代码实现对应的DoBusi方法，而不用修改原来的代码.


