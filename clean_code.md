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

# Naming variables and functions:

- What makes a good name: it's specific enough that someone reading it could understands its purpose and meaning without needing to trace through the logic or check the calling code. It also has to follow the naming convention of the project (camelCase or snake_case) to ensure consistency. Besides, it has to follow basic principles such as functions should be verb-based, variables should be noun-based, and Booleans should be a yes/no question.

- Issues from poor names: wastes developers' or reviewers' time to explain the meaning of each poorly-named variable, increases bug risk (since developers could misuse a variable because of its unclear naming), makes refactoring riskier since it's unclear what a name actually represents, and makes onboarding new team members slower.

- How refactoring improved readability: in the example ("Example of messy code I found on the internet:"), the meaning of "calc(d, r)" is unclear and it makes developers unsure of what is being calculated here. After refining it, the refined function name and parameters: calculateAnnualInterest(principal, monthlyRate) tell you exactly what the function does and what each parameter means, just from the signature so users won't have to read the whole function to understand what it does.


# Writing small, focus functions:

- Why breaking down functions is beneficial: each function would be independently testable and reusable, bugs and errors are easier to be tracked since the big function now were broken into pieces (so you know exactly which function to check), and the top-level function reads like a clear summary of the process instead of a lot of lines of code.

- How refactoring improved structure: the top-level function went from a big chunk of code to meaningfully-named small steps (which are small functions) which forms a readable sequence, helps new developers to understand it rightaway. Each small function can now be tested and reused on its own.

# Avoid code duplication:

## An example of duplicated code
function getActiveUsersReport(users) {
  const active = users.filter(u => u.status === "active");
  const names = active.map(u => u.name.toUpperCase());
  return names.join(", ");
}

function getInactiveUsersReport(users) {
  const inactive = users.filter(u => u.status === "inactive");
  const names = inactive.map(u => u.name.toUpperCase());
  return names.join(", ");
}

## After refactoring it
function getUsersReportByStatus(users, status) {
  const filtered = users.filter(u => u.status === status);
  const names = filtered.map(u => u.name.toUpperCase());
  return names.join(", ");
}

// usage:
getUsersReportByStatus(users, "active");
getUsersReportByStatus(users, "inactive");

- Issues with the duplicated code: the filter/map/join logic was copy-pasted with only the status string changed — if any logic in the function needed to change (for example: sort names, change the separator), you'd have to remember to update it in both places (and potentially many places in a big project). It's very clear that in those cases, it's easy to fix one copy while forgetting the other, causing inconsistent behavior. 

- How refactoring improved maintainability: there's now only a single line of code to build a user report, which means any future change such as new field, different formatting, or different logic happens once and applies everywhere it's used. Moreover, if the developer wanted to add a report for a new status (for example: "pending") requires zero new function, just a new function call.

# Commenting and documentation:

## When you should add comments

- To explain a decision that is not obvious, or business rule (not what the code does)
- Documenting public functions/APIs (parameters, return values, side effects) for other developers using them
- Flagging known limitations, edge cases, or TODOs that aren't obvious from the code itself
- Explaining complex algorithms or math (codes that are not usually understandable by only reading it)

## When you should avoid comments and improve the code instead

- Code lines that have clear meaning and don't need any further explanation (for example: // increment i above i++)
- If you need a comment to explain what a function does, that's usually a sign the function/variable names aren't descriptive enough — rename instead
- If a comment explains a big block of mixed logic, that's often a sign the block should be broken into smaller, well-named functions instead (the function names become the documentation)

# Handling errors & edge cases:
- Example of a function without error handling:

function getDiscountedPrice(price, discountPercent) {
  return price - (price * discountPercent / 100);
}

- After refactoring it: 

function getDiscountedPrice(price, discountPercent) {
  if (typeof price !== "number" || price < 0) {
    throw new Error("price must be a non-negative number");
  }
  if (typeof discountPercent !== "number" || discountPercent < 0 || discountPercent > 100) {
    throw new Error("discountPercent must be a number between 0 and 100");
  }

  return price - (price * discountPercent / 100);
}

- What was the issue with the original code:

- Functions often assume inputs are always valid — no checks for null/undefined, empty arrays, wrong types, or out-of-range values
- Without guard clauses, invalid input either crashes the program with an unhelpful error, or silently produces wrong results (e.g., NaN, an empty object) that surface as bugs much later, far from the actual cause
- Deeply nested if blocks (instead of early returns/guard clauses) make it hard to see what's actually being validated

- How handling errors improves reliability:

- Guard clauses catch bad input immediately at the function boundary, with a clear, specific error message pointing at the real problem
- Failing fast and loud is easier to debug than a silent wrong result that only causes issues downstream
- Makes the function's assumptions explicit — anyone reading it can see exactly what inputs are considered valid, without guessing
- Reduces the "happy path only" nesting, since guard clauses return early and let the main logic stay flat and readable

# Refactoring code for simplicity:

- An example of an overly complicated code:

function getUserStatus(user) {
  if (user != null) {
    if (user.age !== undefined) {
      if (user.age >= 18) {
        if (user.isActive == true) {
          return "active-adult";
        } else {
          return "inactive-adult";
        }
      } else {
        if (user.isActive == true) {
          return "active-minor";
        } else {
          return "inactive-minor";
        }
      }
    }
  }
  return "unknown";
}

- After refactoring it:

function getUserStatus(user) {
  if (!user || user.age === undefined) {
    return "unknown";
  }

  const ageGroup = user.age >= 18 ? "adult" : "minor";
  const activityStatus = user.isActive ? "active" : "inactive";

  return `${activityStatus}-${ageGroup}`;
}

- What made the original code complex: four levels of nested if statements require users to remember all conditions in their head at once when they read the code - which will probably take users longer time to understand it. While it only needs 2 independent boolean checks (age group, activity status) instead of 4 nested if statements like above.

- How refactoring improved it: a guard clause handles the invalid case immediately and exits, flattening the rest of the logic. Extracting ageGroup and activityStatus as named variables makes each condition's meaning explicit, and combining them into one return statement eliminates four duplicate return branches down to one — same behavior, far less code to read and reason about.