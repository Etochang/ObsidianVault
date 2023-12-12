202312070115
Meta Tags: #textbook 
Tags: [[computer organization]]

# Technologies for Building Processors and Memory

Processors and memory have improved at an incredible rate, because computer designers have long embraced the latest in electronic technology to try to win the race to design a better computer. The image below shows the technologies that have been used over time, with an estimate of the relative performance per unit cost for each technology. Since this technology shapes what computers will be able to do and how quickly they will evolve, we believe all computer professionals should be familiar with the basics of integrated circuits.

>[!example] Relative performance per unit cost of technologies used in computers over time.
>![[F000011f01-10-9780128201091.jpg]]

>[!note] transistor
>An on/off switch controlled by an electric signal.

A **transistor** is simply an on/off switch controlled by electricity. The *integrated circuit* (IC) combines dozens to hundreds of transistors into a single chip. When Gordon Moore predicted the continuous doubling of resources, he was predicting the growth rate of the number of transistors per chip. To describe the tremendous increase in the number of transistors from hundreds to millions, the adjective _very large scale_ is added to the term, creating the abbreviation _VLSI_, for **very large-scale integrated circuit**.

>[!note] very large-scale integrated (VLSI) circuit
>A device containing hundreds of thousands to millions of transistors.

This rate of increasing integration has been remarkably stable. The figure below shows the growth in DRAM capacity since 1977. For decades, the industry has consistently quadrupled capacity every 3 years, resulting in an increase in excess of 16,000 times! Figure 1.11 also shows the slowdown due to the slowing of Moore’s Law; quadrupling capacity has taken 6 years recently.

>[!example] **Growth of capacity per DRAM chip over time.**
> ![[F000011f01-11-9780128201091.jpg]]

To understand how manufacture integrated circuits, we start at the beginning. The manufacture of a chip begins with **silicon**, a substance found in sand. Because silicon does not conduct electricity well, it is called a **semiconductor**. With a special chemical process, it is possible to add materials to silicon that allow tiny areas to transform into one of three devices:

- Excellent conductors of electricity (using either microscopic copper or aluminum wire)
- Excellent insulators from electricity (like plastic sheathing or glass)
- Areas that can conduct or insulate under special conditions (as a switch)

>[!note] silicon
> A natural element that is a semiconductor.

>[!note] semiconductor
> A substance that does not conduct electricity well.

Transistors fall in the last category. A VLSI circuit, then, is just billions of combinations of conductors, insulators, and switches manufactured in a single small package.

The manufacturing process for integrated circuits is critical to the cost of the chips and hence important to computer designers. The figure below shows that process. The process starts with a **silicon crystal ingot**, which looks like a giant sausage. Today, ingots are 8–12 inches in diameter and about 12–24 inches long. An ingot is finely sliced into **wafers** no more than 0.1 inches thick. These wafers then go through a series of processing steps, during which patterns of chemicals are placed on each wafer, creating the transistors, conductors, and insulators discussed earlier. Today’s integrated circuits contain only one layer of transistors but may have from two to eight levels of metal conductor, separated by layers of insulators.

>[!note] silicon crystal ingot
> A rod composed of a silicon crystal that is between 8 and 12 inches in diameter and about 12 to 24 inches long.

>[!note] wafer
> A slice from a silicon ingot no more than 0.1 inches thick, used to create chips.

>[!example] **The chip manufacturing process.**
>![[F000011f01-12-9780128201091.jpg]]

A single microscopic flaw in the wafer itself or in one of the dozens of patterning steps can result in that area of the wafer failing. These **defects**, as they are called, make it virtually impossible to manufacture a perfect wafer. The simplest way to cope with imperfection is to place many independent components on a single wafer. The patterned wafer is then chopped up, or _diced_, into these components, called **dies** and more informally known as **chips**. The figure below shows a photograph of a wafer containing microprocessors before they have been diced; earlier, the A12 chip closeup shows an individual microprocessor die.

>[!note] defect
> A microscopic flaw in a wafer or in patterning steps that can result in the failure of the die containing that defect.

>[!note] die
> The individual rectangular sections that are cut from a wafer, more informally known as **chips**.

>[!example] **A 12-inch (300-mm) wafer this 10 nm wafer contains 10th Gen Intel® Core™ processors, code-named “Ice Lake” (Courtesy Intel).**
>![[F000011f01-13-9780128201091.jpg]]

Dicing enables you to discard only those dies that were unlucky enough to contain the flaws, rather than the whole wafer. This concept is quantified by the **yield** of a process, which is defined as the percentage of good dies from the total number of dies on the wafer.

>[!note] yield
> The percentage of good dies from the total number of dies on the wafer.

The cost of an integrated circuit rises quickly as the die size increases, due both to the lower yield and the smaller number of dies that fit on a wafer. To reduce the cost, using the next generation process shrinks a large die as it uses smaller sizes for both transistors and wires. This improves the yield and the die count per wafer. A 7-nanometer (nm) process was state-of-the-art in 2020, which means essentially that the smallest feature size on the die is 7 nm.

Once you’ve found good dies, they are connected to the input/output pins of a package, using a process called _bonding_. These packaged parts are tested a final time, since mistakes can occur in packaging, and then they are shipped to customers.

While we have talked about the cost of chips, there is a difference between cost and price. Companies charge as much as the market will bear to maximize the return on their investment, which must cover costs like a company’s research and development (R&D), marketing, sales, manufacturing equipment maintenance, building rental, cost of financing, pretax profits, and taxes. Margins can be higher on unique chips that come from only one company, like microprocessors, versus chips that are commodities supplied by several companies, like DRAMs. The price fluctuates based on the ratio of supply and demand, and it is easy for multiple companies to build more chips than the market demands.

>[!important] Elaboration
>The cost of an integrated circuit can be expressed in three simple equations:
>![[F000011si1.png]]
>The first equation is straightforward to derive. The second is an approximation, since it does not subtract the area near the border of the round wafer that cannot accommodate the rectangular dies. The final equation is based on empirical observations of yields at integrated circuit factories, with the exponent related to the number of critical processing steps.
>
Hence, depending on the defect rate and the size of the die and wafer, costs are generally not linear in the die area.

>[!warning] Check Yourself
>A key factor in determining the cost of an integrated circuit is volume. Which of the following are reasons why a chip made in high volume should cost less?
>1. With high volumes, the manufacturing process can be tuned to a particular design, increasing the yield.
>2. It is less work to design a high-volume part than a low-volume part.
>3. The masks used to make the chip are expensive, so the cost per chip is lower for higher volumes.
>4. Engineering development costs are high and largely independent of volume; thus, the development cost per die is lower with high-volume parts.
>5. High-volume parts usually have smaller die sizes than low-volume parts and therefore have higher yield per wafer.

# [[Performance]]



---
# *References*