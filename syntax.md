# Syntax for Webchart Tool

## Basic Concept

### Blocks

There are 3 types of blocks, they are:

1. Terminator: 

   The terminator usually represents the 'start' or the 'end' of a process. It's a rectangle with round corners.

   <img src="docs/_image/file%20(12).svg" alt="file (12)" style="zoom:50%;" />

   `T` or `Terminator` can be used to represent `Terminator ` and it's case incensitive. 

2. Process:

   The process block usually represents a workflow activity. It's a rectangle.

   <img src="docs/_image/file%20(13).svg" alt="file (13)" style="zoom:50%;" />

   You can input `p` or `Process` when creating the flow chart.

3. Decision:

   The decision shape usually represents different choices in a workflow.

   <img src="docs/_image/file%20(14).svg" alt="file (14)" style="zoom:50%;" />

   You can input `d` or `Decision` when creating the flow chart.

4. How to input a block

   A block always starts with its short indicator and follows with a `:`. All of its content will be in a closed paprentasises. For example:

   ```
   p:("This is a process")
   t:("Start")
   d:("Choices")
   ```

   A process with all possible elements will look like:

   ```
   p:("solution design", id:p1, from:{p0, label:go,stroke:red},stroke:green, fill:blue)
   ```

   Each element will be explained below.
   
4. Multiple blocks within one row

   Multiple blocks within the same row can be seperated by `;`. For example:

   ```
   p:("Reading");p("Writing")
   ```
   
   <img src="docs/_image/file%20(16).svg" alt="file (16)" style="zoom:67%;" />

4. Multiple blocks in different rows

   For example:

   ```
   p:("Reading")
   p:("Writing")
   ```
   
   <img src="docs/_image/file%20(17).svg" alt="file (17)" style="zoom:67%;" />
   
4. Position multiple blocks

   You can combine the row and the letter of `;` to position blocks differently. For example:

   ```
   ;t:("Start");
   p:("Let's go");
   ;;p:("what else")
   ```

   <img src="docs/_image/file%20(18).svg" alt="file (18)" style="zoom:67%;" />

## Key element in each blocks.

### Block Label

The first element within the parentasis of a block is default as the label of the block (terminator, process or decision). It can accept any unicode and it also accepts special charactors which needs to be escaped. They are: 

| Input | Represent | Note |
| ----- | --------- | ---- |
| \n    | new line  |      |
| \t    | tab       |      |
| \\\\  | \         |      |
| \\'   | '         |      |
| \\"   | "         |      |

For examples (pay attention to the `\n` in the middle of the label):

```
p:("Finish the UI design\nin the weekend")
```

<img src="docs/_image/file%20(19).svg" alt="file (19)" style="zoom:67%;" />

### ID

`ID` is almost the second important element of a block. It's optional though. However, you can't reference the block from another block if it misses a `ID`. It will not change any visible shape. For example:

```
p:("Finish the UI design\nin the weekend", id:p1)
```

When you input, you have free choices to use `ID` or `Id` or `id`. The value of the `ID` must be unique or you can't reuse the `ID` value in a different block.

It will be explained more in next.

### `From` and `To`

`From` and `To` elements are used to create connections between blocks. A connection between two blocks can be either created through a `from` element in the target block or a `to` element in the source block. For example:

```
p:("Design",id:p1);p:("Play Game", from:{p1})
```

Or:

```
p:("Design", to:{p2});p:("Play Game", id:p2)
```

Both of them will have the same visualization result: a line connected two blocks from the right to the left.

<img src="docs/_image/file%20(20).svg" alt="file (20)" style="zoom:67%;" />

```
p:("Design",id:p1)
;p:("Play Game", from:{p1})
```

or:

```
p:("Design", to:{p2})
;p:("Play Game", id:p2)
```

<img src="docs/_image/file%20(21).svg" alt="file (21)" style="zoom:67%;" />

Both `from` and `to` can be simplified when there is only one element, the `id`.  For example:

```
p:("Design",id:p1)
;p:("Play Game", f:p1)
```

The `f:p` equals to `from:{p1}`. The same rule applies to the `to` element.

Each `From` or `To` element can have different elements too, which will be explained later.

### `Stroke` and `Fill`

The `stroke` element will assign a different color the border of each block. The border color will be in black by default. The `fill` element will define the color to fill in the block and the default is white. For example:

```
;t:("Start",stroke:red)
p:("Green", fill:green);;p:("Blue",fill:orange,stroke:blue)
```

<img src="docs/_image/file%20(22).svg" alt="file (22)" style="zoom:67%;" />

## Key Elements in each `from` and `to`

### Stroke

This element will change the default color of a connection, which has a black color by default. For example:

```
p:("Start",id:p1);p:("End",from:{p1,stroke:red})
```

<img src="docs/_image/file%20(23).svg" alt="file (23)" style="zoom:67%;" />

### `Label`

This is almost the most important element of a connection. see example:

```
p:("start",id:p1);;p:("end", from:{p1,label:lucky})
```

<img src="docs/_image/file%20(24).svg" alt="file (24)" style="zoom:67%;" />

You can only input `l` to represent a label, for example:

```
p:("start",id:p1);;p:("end", from:{p1,l:lucky})
```



### `Label_from` and `Label_to`

`Label_from` and `Label_to` will put a text explanation on either the beginning side or the end side of a connection. For example:

```
p:("start",id:p1);;p:("end", from:{p1,label_from:pray,label_to:lucky})
```

<img src="docs/_image/file%20(25).svg" alt="file (25)" style="zoom:67%;" />

`Label_from` can be input as short as `lf`.`Label_to` can be input as short as `lt`.

## Layout control

This tool is aiming to use in a simple way and the most development energy is spent in the auto layout capability. Basically, you only have two ways to decide where a block should be:

1. Different row to move the block up or down.
2. `;` move the block left or right.



The connection between blocks are fully automated and you have no way to control it. The current algorithm can avoid the most cases of a line to across another line, but it can't prevent all of the cases yet.

For example:

```
p:("calculate the gcd\nof a and b",id:p0)
p:("find remainder\nr of a/b",id:p1,from:{p0})
d:("r=0?",id:p2,from:{p1});p:("a <-- b\nb <-- r",id:p3,from:{p2,l:no},to:{p1})
p:("the gcd is b",from:{p2,label:yes})
```

<img src="docs/_image/file%20(27).svg" alt="file (27)" style="zoom:67%;" />
