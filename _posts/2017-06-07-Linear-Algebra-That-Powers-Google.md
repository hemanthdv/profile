## Introduction

The world wide web (web) is a humongous library with nearly 60 trillion pages (we refer to a web-page as page). It is constantly growing with pages being added at an ever increasing rate. There is no apparent catalog that tracks these pages. It would be nearly impossible to search the web without a librarian's help. Web Search Engines (WSE) are the librarians of the web. Based on a search query, they precisely direct us to the material of interest. The most popular WSE are Google, Bing, Baidu and Yahoo.

It is a tremendous challenge to track all the information on the web and access it at a moments notice. This article briefly outlines the techniques deployed by the Google Search Engine (GSE) to achieve this feat. We will study in some detail the PageRank algorithm that ranks pages based on their importance. In the process, we will also discover how basic concepts in Linear Algebra like the eigenvalue problem and the power method, are the running force behind the \$400 billion Google empire.

## Beneath Google's Surface

### Crawling and Indexing

Google gathers information from the web using programs called web crawlers. Google's popular web crawlers (Googlebots) visit pages and gather information. They follow links on a page to reach other pages. In this manner web crawlers gather information from the entire public accessible web. The [crawler](#insideGoogleSearch) pays attention to new pages, dead links and changes to existing pages. Websites can choose if they wish to be crawled or not. An indexing program (indexer) goes through each word in every page and notes the number of **hits** (occurrences) for each word on the page. It also keeps track of font size and the use of bold and underline that denotes importance . The indexer assigns a unique **DocID** to the page and a snippet describing the page is generated which is used when displaying search [results](#hillInside). All of this information is dumped into **barrels** for later access. Google's index of the web is nearly [100 Tera bytes](#insideGoogleSearch).

### Algorithms

When a set of words is entered as a search query, algorithms try to make sense of the user input. These include algorithms for spelling, synonyms, auto-complete and query-understanding. The number of occurrences of the search words in the page and their position is also considered. A list of pages is then accessed from the index. A typical query often results in millions of pages. Google's algorithms sort these pages in the order of relevance. More than 200 criteria are used to filter and order [these pages](#insideGoogleSearch). Some of them are freshness of content, user context, spam-filtering, your region and PageRank. The most relevant pages end up as results on your computer. All of this happens in \\({\frac{1}{8}}^{th}\\) of a second.

## Page Rank Algorithm

### Which Page is Important

The PageRank algorithm, as the name indicates, orders pages based on their importance. It was developed by the founders of Google, [Sergey Brin and Lawrence Page](#page1999pagerank). The PageRank algorithm judges the importance of a page by the number of other important pages that refer (link) to it. Let us assume a web of interest that contains \\(N\\) pages \\(\{p_1,\ldots,p_k,\ldots,p_N\}\\) as in Figure. \ref{graph1}. We use the same example from [Bryan and Leslie](#bryan200625) for ease of understanding. We will use \\(x_k \geq 0\\) to denote the importance of a page \\(p_k\\), and \\(x_i > x_j\\) implies that \\(p_i\\) is more important than \\(p_j\\). We represent our web as a directed graph with nodes as pages and edges as hyperlinks between them. The simplest way to assess the importance of a page is to set \\(x_k\\) as the number of backlinks (hyperlinks pointing to the page) to page \\(p_k\\). In our web example we get \\(x_1=2, x_2=1, x_3=3, x_4=2\\). This approach treats all backlinks with equal importance. A link from an important page say, www.cnn.com ought to be treated with more importance than a link from a lesser important page, like your home page. To incorporate this idea let us assume the importance \\(x_k\\) to be the weighted sum of the importances of pages linking to it. More specifically, if page \\(p_j\\) has \\(n_j\\) outgoing links to other pages, it gives importance \\(x_j/n_j\\) to each of those links. Therefore, the importance of page \\(p_k\\) with \\(L_k\subset\{p_1,\ldots,p_N\}\\) pages linking to it is given by,
<br />
<br />
<img align="middle" width="500" src="{{ site.url }}/images/GoogleLA_graph1.png" alt="...">

A web with four pages and links between them.
<br />
<br />
\\[
x_k = \sum_{p_j\in L_k}x_j/n_j
\\]
In this setup, we will not count self-referencing links. In our web example, \\(x_1 = x_3/1 + x_4/2\\) with \\(p_3\\) giving all its importance to just one link and \\(p_4\\) sharing its importance with \\(p_1\\) and \\(p_3\\). Similarly, \\(x_3 = x_1/3 + x_2/2 + x_4/2\\). We can represent this as a set of linear equations \\(A\mathbf{x} = \mathbf{x}\\) where, \\(\mathbf{x} = [x_1,x_2,x_3,x_4]^\top\\) and,
\\[
A =
\begin{bmatrix}
0 & 0 & 1 & \frac{1}{2}\newline
\frac{1}{3} & 0 & 0 & 0\newline
\frac{1}{3} & \frac{1}{2} & 0 & \frac{1}{2}\newline
\frac{1}{3} & \frac{1}{2} & 0 & 0
\end{bmatrix}
\\]
We refer to \\(A\\) as the **link matrix**. The above equation is a standard eigenvalue problem \\(A\mathbf{x} = \lambda\mathbf{x}\\) where we need to estimate the eigenvector \\(\mathbf{x}\neq 0\\) for eigenvalue \\(\lambda= 1\\). Matrix \\(A\\) is called **column-stochastic** because each of its columns sum to 1. Since \\(A^\top\mathbf{1} = \mathbf{1}\\), where \\(\mathbf{1}\\) is a vector of all 1's, \\(A\\) has an eigenvalue, \\(\lambda=1\\) (\\(A\\) has the same eigenvalues as \\(A^\top\\) - a matrix property). The corresponding eigenvector \\(\mathbf{x}\\), for \\(A\mathbf{x} = \mathbf{x}\\) is the vector of page ranks. The \\(l_1\\)-normalized PageRank eigenvector for our example turns out to be, \\(\mathbf{x} = [0.38, 0.12, 0.29,0.19]^\top\\). We apply \\(l_1\\)-normalization so that \\(\sum_k x_k=1\\). We now need to ensure that \\(\mathbf{x}\\) is unique. This is where we run into problems for some cases.

### Non-Unique PageRank and Dangling Nodes
Let \\(V_1(A)\\) be the eigenspace for \\(\lambda=1\\). The number of distinct eigenvectors for \\(\lambda=1\\) or dim(\\(V_1(A)\\)) is equal to the number of disconnected components in the graph. A strongly connected graph (can visit any node from any other node in a finite number of steps) has a unique eigenvector for \\(\lambda=1\\). Consider a different web graph as depicted in Figure. \ref{graph2}. The link matrix yields two distinct eigenvectors for \\(\lambda=1\\). It is not clear which of these eigenvectors(or their linear combination) is the best page rank. The other difficulty comes with dangling nodes - pages that do not link to any other pages. These pages have a column of all zeros in the link matrix which is now termed **column-substochastic** (column sum \\(\leq\\) 1). The eigenvalues of a column-substochastic matrix have \\(\lambda\leq 1\\) and 1 need not be an eigenvalue. The eigenvector for the largest eigenvalue also need not be strictly positive.
<br />
<br />
{% include image.html url="{{ site.url }}/images/GoogleLA_graph2.png" description="A web with disconnected components." %}
<br />
<br />

Brin and Page came up with a simple solution for the non-unique PageRank problem which we now outline. Let \\(A\\) be a link matrix for a web with no dangling nodes. We define a new column-stochastic matrix given by,
\\[
M = (1-m)A + mS
\label{eq2}
\\]
\\(M\\) is the new link matrix and \\(S\\) is a \\(N\times N\\) matrix with all entries equal to \\(1/N\\) and \\(m\in[0,1]\\). The intuition behind adding matrix \\(S\\) is to make the graph strongly connected. The link matrix for such a graph is said to be **primitve**. We will see the need for this in the following subsection. In our case \\(M\\) is primitive and **irreducible**. An irreducible link matrix yields non zero entries in the PageRank vector. When a graph has no "importance sink" that drains the importance of other nodes, its link matrix is [irreducible](#austin2006google). In other words, there is no subgraph which has zero outgoing links. We will not deal with the dangling node problem as it is beyond scope. We mention in passing that "lumping" all the dangling nodes into a single node and calculating the PageRank for the rest of the web is one way to deal with [dangling nodes](#danglingSol).

### Power Method
The world wide web consists of nearly 60 trillion (tr) pages. Its link matrix is [\\(60tr \times 60tr\\)]. It is infeasible to find its eigenvector by standard techniques. This is where the power method comes handy. Beginning with \\(\mathbf{x}_0\\) (a random non zero vector), \\(\mathbf{x}_n = M^n\mathbf{x}_0\\) converges to a unique stationary eigenvector when \\(n\\) tends to \\(\infty\\) for a column stochastic matrix \\(M\\). For the power method to converge, the dimension of the eigenspace for the largest eigenvalue must be 1. This condition is satisfied when the link matrix is primitive. Although we do not have to solve the eigenvalue problem, we still got to do \\(\mathcal{O}(N^2)\\) multiplications in every iteration. But, Equation \\ref{eq2} can be simplified to \\(M\mathbf{x} = (1-m)A\mathbf{x} + m\mathbf{s}\\), where \\(\mathbf{s} = S\mathbf{x}\\), is a vector with all entries \\(1/N\\) when \\(\mathbf{x}\\) is positive and \\(||\mathbf{x}||\_1 = 1\\). Since \\(A\\) is highly sparse, this computation is now [efficient](#bryan200625).

## Conclusion
Google has been constantly innovating and improving its Search Engine technology. Projects like Knowledge Graph, Google Instant, Query understanding etc. are some recent technologies added to the GSE. Apart from PageRank, there are also other equally efficient algorithms that use link analysis to arrive at page ranking. The most prominent being the HITS algorithm developed by [Jon Kleinberg](#hits) that is used in the www.Ask.com Search Engine. Linear Algebra plays an important role in most of the link analysis algorithms. It would be an interesting exercise in Linear Algebra and Data Mining to program a Search Engine for a relational database.

## References
<a name="austin2006google">Austin, D., 2006. How Google finds your needle in the web's haystack, American Mathematical Society Feature Column.

<a name="bryan200625">Bryan, B., and Leise, T., 2006. The \$25,000,000,000 eigenvector: The linear algebra behind Google, Siam Review.

<a name="insideGoogleSearch"> Google: Inside Search, http://www.google.com/intl/en_us/insidesearch/

<a name="hillInside">Hill, A., April, 2004. Google Inside Out, Maximum PC.

<a name="hits">Kleinberg, J., December, 1999. Hubs, Authorities, and Communities, Cornell University.

<a name="danglingSol">Lee, C. P., Golub, G. H., and Zenios, S. A., 2003. A Fast Two-Stage Algorithm for Computing PageRank and Its Extensions, Stanford University.

<a name="page1999pagerank"> Page, L., Brin, S., Motwani, R., and Winograd, T., 1999. The PageRank citation ranking: Bringing order to the web, Stanford InfoLab.
