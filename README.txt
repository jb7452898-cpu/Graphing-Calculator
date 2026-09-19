first iteration worked but couldnt create a solution
The most common reason for a "Not Equivalent" error when typing a solution like x = 4 comes down to how equation equivalence is evaluated: 2x + 6 = 14 is an equation comparing two functions, whereas x = 4 is a fixed constant constraint (a vertical line at $x = 4$).When subtracting the sides of an equation:For 2(x + 3) = 14, subtracting the right side gives $f(x) = 2x + 6 - 14 = \mathbf{2x - 8}$.For x = 4, subtracting the right side gives $g(x) = \mathbf{x - 4}$.Because $2x - 8 \neq x - 4$ for every $x$, sample-point testing marks them as non-equivalent functions, even though they share the exact same root ($x = 4$).

key adjustments
1. check if roots/zero crossings match or if one is scalar multiple of the other
2. special handling for direct variable assignments

What’s Included in This Updated VersionQuadratic Equations:Automatic support for exponents (e.g., x^2 - 5x + 6 = 0 or (x-1)^2 = 4).Roots are dynamically solved using quadratic roots/zero-crossings ($x = 2$, $x = 3$).Plots curves (parabolas) and marks roots on the canvas with vertical guide lines.Systems of Linear Equations:Multi-line problem targets (e.g., Line 1: 2x + y = 7, Line 2: x - y = 1).Computes the linear intersection point $(x, y)$ using matrix solver methods (math.lusolve).Workspace equivalence verification works for individual lines.Workspace solution trigger checks for exact coordinate targets like x = 2, y = 3 or (2, 3).Graphically renders both system lines and draws a point at their intersection.

cant group solutions using a comma
That happening because the parser expects an equals sign (=) on every workspace line, so a plain coordinate pair like (2.67, 1.67) or a line without a second equals sign triggers an Invalid Format check.

To fix this, we can update the workspace line parser so it recognizes both:

    Multiple variable assignments on one line: x = 2.67, y = 1.67

    Coordinate point syntax: (2.67, 1.67) or (x, y) = (2.67, 1.67)

The Fix

In your index.html, locate the processAll() function inside the <script> tag and update the workspace loop section with this logic:

got x = something, y = something to work
(something, something)  still does not

The issue with coordinate syntax like (2.67, 1.67) happens because math.parse("(2.67, 1.67)") creates a multi-element Matrix node, which breaks during the equation check and triggers an Invalid Format or Syntax Error.

To fix this, we need to explicitly recognize coordinate pairs before passing the string to math.parse().

Here is the updated processAll()
