## Intro 102

Asoteric lets the developer write the rules that would unambiguiosly parse each of the above queries into a perfectly explainable and visualizable representation, which we call the meaning tree.

One problem that greatly illustrates the importance of perfect parsing is understanding free-form dates. In fact, the open source part of Asoteric includes not only the engine itself, but also the rule set for date parsing, and the live demo that is publicly available *here*. **TODO(dkorolev)**: Publish it.

More complex example queries where Asoteric rocks:

* `place an order to buy 100 shares of MSFT limit at 250`
* `can paracetamol be prescribed to patients with type 2 diabetes?`
* `show files modified yesterday that are under version control and were last pushed over a year ago`
* `show products sold by the sales departments in the caribbean which have drained the stock by over 50% last month`
* `which counties of at least 10k population, median age above 40, voted against prop 42, have more covid cases in march?`
* `bump jira ticket 4242 to p1 for the build cycle that goes to qa next tuesday, and notify the pms whose teams are affected`

The meaning tree is a [JSON] object that follows the strong schema defined by the developer. The meaning tree hierarchically outlines the way the system has understood the query. The meaning tree is the natural extension of the parse tree, which only captures the exact grouping of terms into specifig parsing rules that were matched. The meaning tree augments the parse tree with everything else that the author of the grammar has put into it.

In many cases this meaning tree would lead directly to answering the end user's question.

For example, when parsing dates, the meaning tree itself contains the Unix epoch timestamps describing what the query is referring to. In the trading vocabilary example above, not only the notion of the limit order, but also that `MSFT` is a stock sticker and that 250 is $250 USD, is encoded into the rules set that construct the meaning tree.

In the cases where the developer has elected to not put everything into the grammar, the Asoteric output is then consumed by the invoking party to generate and present the ultimate output of what the user is looking for.

In all cases, the end user would get to confirm, in an intuitive way, that the system has understood their request in the way intended.
