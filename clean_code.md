# Clean code principles:

- Simplicity — solve the problem while keeping it as simple as possible (avoid complexity). Also, avoid clever one-liners or unnecessary abstraction layers that make code harder to follow than a plain, direct approach
- Readability — code is read far more often than it's written. Thus follow these principles to improve the code's readability: use descriptive names, consistent formatting, and small functions so intent is obvious without extensive comments
- Maintainability — structure code so future changes (bug fixes, new features) are easy and low-risk — avoid tight coupling, magic numbers, and duplicated logic scattered everywhere
- Consistency — strictly follow the project's or team's style guide and naming conventions (naming, indentation, file structure) even if changing to another style would fit your brainstorming process more and could improve your work performace. Have to keep in mind that consistency across a codebase matters more than individual preference
- Efficiency — write reasonably performant code, but don't over-optimize prematurely at the cost of readability (have to balance between efficiency and readability of the codebase). Optimize only where profiling shows it actually matters

## Example of messy code I found on the internet:

function p(a,b,c){
let x=[];for(let i=0;i<a.length;i++){if(a[i].t=="x"&&a[i].s>b){x.push(a[i])}}
if(c==1){x.sort(function(m,n){return n.s-m.s})}
return x
}

- Why it's hard to read: names don't have meanings (p, a, b), no spacing or formatting (no indent) - affects readability, no comments, filtering and sorting logic mixed into 1 line with no formatting.

## How I would refine it:
function getExpiredItemsAboveThreshold(items, scoreThreshold, sortDescending) {
  const EXPIRED_STATUS = "x";

  const filteredItems = items.filter(
    (item) => item.status === EXPIRED_STATUS && item.score > scoreThreshold
  );

  if (sortDescending) {
    filteredItems.sort((a, b) => b.score - a.score);
  }

  return filteredItems;
}

