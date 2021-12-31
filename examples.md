# Examples Created By Webchart Tool

1. Example 1

   Code:

   ```
   p:("calculate the gcd\nof a and b",id:p0)
   p:("find remainder\nr of a/b",id:p1,from:{p0})
   d:("r=0?",id:p2,from:{p1});p:("a <-- b\nb <-- r",id:p3,from:{p2,l:no},to:{p1})
   p:("the gcd is b",from:{p2,label:yes})
   
   ```

   SVG:

   ![output](docs/_image/output.svg)

2. Example 2

   Code:

   ```
   ;Terminator:("Start",Id:P0,To:{P1});
   ;Process:("Prepare for the day\nNo more Delay!",Id:P1,To:{P2,Label:Demo},To:{P3},To:{P4,Label:"Right Above"});
   Process:("P2 Storage",Id:P2);Process:("Demo P3",Id:P3,To:{P4},To:{P5});Process:("Demo P4",Id:P4)
   ;Process:("P5 Demo",Id:P5,From:{P2,Label_From:"To P5",Label:"Demo P2",Label_To:"From P2"},From:{P3},From:{P1,Label_From:"To P5",Label:"Rotate 90"});Process:("Do something else",Id:P6,From:{P2},From:{P4})
   ;Terminator:("Good End",Id:P7,From:{P5},From:{P6});  
                 
   ```

   SVG:

   ![output](docs/_image/output-0986902.svg)

3. Example 3:

   Code:

   ```
   ;Terminator:("Start",Id:P0);
   ;Process:("What do you do \nin holiday",Id:P1,From:{P0});
   Process:("Gaming",Id:P2,From:{P1});;Process:("Eating",Id:P3,From:{P1})
   ;Process:("What else",Id:P4,From:{P1});
   ;Terminator:("End",From:{P2,Label:"any bug"},From:{P3,Label:"who knows"},From:{P4,Label:"don't know"});
   ```

   SVG:

   ![output](docs/_image/output-0986938.svg)

4. 
