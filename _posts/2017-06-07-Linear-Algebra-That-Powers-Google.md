<head>
...
    <script type="text/javascript"
            src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
    </script>
...
</head>
## Introduction

The world wide web (web) is a humongous library with nearly 60 trillion pages (we refer to a web-page as page). It is constantly growing with pages being added at an ever increasing rate. There is no apparent catalog that tracks these pages. It would be nearly impossible to search the web without a librarian's help. Web Search Engines (WSE) are the librarians of the web. Based on a search query, they precisely direct us to the material of interest. The most popular WSE are Google, Baidu, Yahoo and Bing.

It is a tremendous challenge to track all the information on the web and access it at a moments notice. This article briefly outlines the techniques deployed by the Google Search Engine (GSE) to achieve this feat. We will study in some detail the PageRank algorithm that ranks pages based on their importance. In the process, we will also discover how basic concepts in Linear Algebra like the eigenvalue problem and the power method, are the running force behind the \$400 billion Google empire.

## Beneath Google's Surface

### Crawling and Indexing

Google gathers information from the web using programs called web crawlers. Google's popular web crawlers (Googlebots) visit pages and gather information. They follow links on a page to reach other pages. In this manner web crawlers gather information from the entire public accessible web. The [crawler](#insideGoogleSearch) pays attention to new pages, dead links and changes to existing pages. Websites can choose if they wish to be crawled or not. An indexing program (indexer) goes through each word in every page and notes the number of *hits* (occurrences) for each word on the page. It also keeps track of font size and the use of bold and underline that denotes importance . The indexer assigns a unique *DocID* to the page and a snippet describing the page is generated which is used when displaying search [results](#hillInside). All of this information is dumped into *barrels* for later access. Google's index of the web is nearly [100 Tera bytes](#insideGoogleSearch).

### Algorithms

When a set of words is entered as a search query, algorithms try to make sense of the user input. These include algorithms for spelling, synonyms, auto-complete and query-understanding. The number of occurrences of the search words in the page and their position is also considered. A list of pages is then accessed from the index. A typical query often results in millions of pages. Google's algorithms sort these pages in the order of relevance. More than 200 criteria are used to filter and order [these pages](#insideGoogleSearch). Some of them are freshness of content, user context, spam-filtering, your region and PageRank. The most relevant pages end up as results on your computer. All of this happens in ${1/8}^{th}$ of a second.

## Page Rank Algorithm

### Which Page is Important

The PageRank algorithm, as the name indicates, orders pages based on their importance. It was developed by the founders of Google, [Sergey Brin and Lawrence Page](#page1999pagerank). The PageRank algorithm judges the importance of a page by the number of other important pages that refer (link) to it. Let us assume a web of interest that contains $N$ pages \(\{p_1,\ldots,p_k,\ldots,p_N\}\) as in Figure. \ref{graph1}. We use the same example from [Bryan and Leslie](#bryan200625) for ease of understanding. We will use $x_k \geq 0$ to denote the importance of a page $p_k$, and $x_i > x_j$ implies that $p_i$ is more important than $p_j$. We represent our web as a directed graph with nodes as pages and edges as hyperlinks between them. The simplest way to assess the importance of a page is to set $x_k$ as the number of backlinks (hyperlinks pointing to the page) to page $p_k$. In our web example we get $x_1=2, x_2=1, x_3=3, x_4=2$. This approach treats all backlinks with equal importance. A link from an important page say, www.cnn.com ought to be treated with more importance than a link from a lesser important page, like your home page. To incorporate this idea let us assume the importance $x_k$ to be the weighted sum of the importances of pages linking to it. More specifically, if page $p_j$ has $n_j$ outgoing links to other pages, it gives importance $x_j/n_j$ to each of those links.

## References
<a name="austin2006google">Austin, D., 2006. How Google finds your needle in the web's haystack, American Mathematical Society Feature Column.

<a name="bryan200625">Bryan, B., and Leise, T., 2006. The \$25,000,000,000 eigenvector: The linear algebra behind Google, Siam Review.

<a name="insideGoogleSearch"> Google: Inside Search, http://www.google.com/intl/en_us/insidesearch/

<a name="hillInside">Hill, A., April, 2004. Google Inside Out, Maximum PC.

<a name="hits">Kleinberg, J., December, 1999. Hubs, Authorities, and Communities, Cornell University.

<a name="danglingSol">Lee, C. P., Golub, G. H., and Zenios, S. A., 2003. A Fast Two-Stage Algorithm for Computing PageRank and Its Extensions, Stanford University.

<a name="page1999pagerank"> Page, L., Brin, S., Motwani, R., and Winograd, T., 1999. The PageRank citation ranking: Bringing order to the web, Stanford InfoLab.
