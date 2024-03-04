# Content/概念

**模式匹配**：允许我们将一个`target`**值**与一系列的**模式**相比较，并根据相匹配的模式执行对应的**表达式**。Rust 中常见的模式匹配有 `match` 和`if let` 两种，这里我们以 match 举例来看看什么是模式匹配。

```java
match target {
    模式1 => 表达式1,
    模式2 => {
        语句1;
        语句2;
        表达式2
    },
    _ => 表达式3
}
```

> 需要注意的是：`match`的匹配必须要穷举出所有可能，因此这里用`_`来代表未列出的所有可能性。
> 
- 比喻
    
    想象你在驾驶汽车时遇到交通信号灯。交通信号灯有三种颜色：红色、绿色和黄色。使用匹配模式，你可以根据信号灯的颜色采取不同的行动：红色，停车；绿色，继续行驶；黄色，减速。在这个例子中，不同颜色的交通信号灯就像不同的枚举，而匹配模式则帮助你根据信号灯的状态采取相应的行动。
    
- 真实用例
    
    我们看这段 solana 中的关于电影评论的程序，用户可以为电影新增评论，也可以修改评论：
    
    ```rust
    // 用户操作的指令类型，为枚举
    pub enum MovieInstruction {
    		// 新增电影评论
        AddMovieReview {
            title: String,
            rating: u8,
            description: String,
        },
    		// 修改电影评论
        UpdateMovieReview {
            title: String,
            rating: u8,
            description: String
        }
    }
    
    pub fn unpack(input: &[u8]) -> Result<Self, ProgramError> {
    		// 实际是根据入参input来赋值
    		let variant = 1;
    		let payload;
    
    		// 模式匹配
    		Ok(match variant {
    		    0 => MovieInstruction::AddMovieReview {
    		        title: payload.title,
    		        rating: payload.rating,
    		        description: payload.description,
    		    },
    		    1 => MovieInstruction::UpdateMovieReview { 
    		        title: payload.title, 
    		        rating: payload.rating, 
    		        description: payload.description 
    		    },
    				// 这里要覆盖到其他情况
    		    _ => return Err(ProgramError::InvalidInstructionData),
    		})
    }
    ```
    

### Documentation

这里使用 `match` 去匹配`BlockChain`的枚举类型，在 match 中使用三个匹配分支来完全覆盖枚举变量 BlockChain 的所有成员类型。

```solidity
enum BlockChain {
    BitCoin,
    Ethereum,
    Starknet,
    Solana,
}

fn main() {
    let block_chain = BlockChain::Solana;
    match block_chain {
        BlockChain::BitCoin => println!("BitCoin"),
        // X | Y，类似逻辑运算符 或，代表该分支可以匹配 X 也可以匹配 Y，只要满足一个即可
        BlockChain::Ethereum | BlockChain::Starknet => {
            println!("Ethereum or Starknet");
        },
        // 使用 _ 来代表未列出的所有可能性
        _ => println!("Solana"),
    };
}
```

### FAQ

# Example/示例代码

这里我们展示下 `match`模式匹配的其他用法：模式绑定、赋值、解构。`if let` 简单模式匹配：用来处理只匹配一个模式的值而忽略其他模式的情况，可以让我们的代码更加简洁。

```solidity
enum Shape {
    Circle(f64),
    Rectangle(f64, f64),
    Square(f64),
}

fn calculate_area(shape: &Shape) -> f64 {
    match shape {
        // 从匹配的模式中取出绑定的值，如radiux、width、side        
        Shape::Circle(radius) => std::f64::consts::PI * radius * radius,
        Shape::Rectangle(width, height) => width * height,
        Shape::Square(side) => side * side,
    }
}
struct Point {
    x: i32,
    y: i32,
}

fn process_point(point: Point) {
    match point {
        Point { x: 0, y: 0 } => println!("坐标在原点"),
        Point { x, y } => println!("坐标在 ({}, {})", x, y),
    }
}

fn main() {
    let circle = Shape::Circle(3.0);
    let rectangle = Shape::Rectangle(4.0, 5.0);
    let square = Shape::Square(2.0);

    // 1、调用函数，输出各形状的面积
    println!("圆形的面积：{}", calculate_area(&circle));
    println!("矩形的面积：{}", calculate_area(&rectangle));
    println!("正方形的面积：{}", calculate_area(&square));

    // 2、match 模式匹配进行赋值
    let area = match circle {
        Shape::Circle(radius) => std::f64::consts::PI * radius * radius,
        Shape::Rectangle(width, height) => width * height,
        Shape::Square(side) => side * side,
    };
    println!("圆形的面积：{}", area);

    // 3、解构结构体
    let point1 = Point { x: 0, y: 0 };
    let point2 = Point { x: 3, y: 7 };
    process_point(point1);
    process_point(point2);

		// 4、if let简单匹配
    let some_u8_value = Some(3u8);
    match some_u8_value {
        Some(3) => println!("three"),
        // 这里还要考虑除 3 以外的其他值，以及None值
        _ => (),
    }
    
    // 只匹配数值 3 即可
    if let Some(3) = some_u8_value {
        println!("three");
    }
}
```