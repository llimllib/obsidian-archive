https://basta.substack.com/p/no-sacred-masterpieces
(the excel for the web: https://github.com/WebSheets/websheets)

> “Hey guys. I’m working on the driver incentive spreadsheet. I’m trying to mimic the calculations that you have in Excel, but my numbers are all just a little bit off. I was hoping you might have some ideas about what’s going on.”

> “Can I take a look?” I showed him my laptop and he played with a few numbers in the inputs. “Oh, that’s the circ.”

> “The ‘circ’?”

> Another data scientist looked up, “The circular reference.”

> “I’m sorry?”

> “We use a circular reference in Excel to do linear regression.”

> My mind was blown. I had thought, naively perhaps, that circular references in Excel simply created an error. But this data scientist showed me that Excel doesn’t error on circular references—if the computed value of the cell converges.

> You see, when formulas create a circular reference, Excel will run that computation up to a number of times. If, in those computations, the magnitude of the difference between the most recent and previous computed values for the cell falls below some pre-defined epsilon value (usually a very small number, like 0.00001), Excel will stop recomputing the cell and pretend like it finished successfully.

Good story with several twists and turns, and also an MIT web component that came out of it.