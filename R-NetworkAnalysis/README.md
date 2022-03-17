# Welcome to the Ramirez Lab Wiki - Graph Theory on Network Analysis

<div align="justify">Here we present a R-Studio pipeline to compute some topological parameters that will help us understand the "relevance" of each node in a protein-protein or drug-protein interaction network in terms of its connections. We are also going to conduct a cut analysis, in order to see which nodes on a network generate a disconnection of components when eliminated. For further information about Topological network analysis go to EMBL-EBI online tutorial: <a href="https://www.ebi.ac.uk/training/online/courses/network-analysis-of-protein-interaction-data-an-introduction/network-analysis-in-biology/" target="_blank"><b>Network analysis of protein interaction data</b></a>.</div>


## Requirements
+ R v4.1.1 or more recent.
+ Input file available in media folder: Input-DPI.xlsx

## Topological Analysis

The first step is installing in R the packages that are needed as well as loading their respective libraries. In order to do this, you can copy and paste the following code in R and run it.

```R
    install.packages("igraph")
    install.packages("ggplot2")
    install.packages("ggraph")
    install.packages("ggvenn")
    install.packages("VennDiagram")
    install.packages("gplots")
    install.packages("UpSetR")
    install.packages("tidyverse")
    install.packages("readxl")


    library(igraph)
    library(ggplot2)
    library(ggraph)
    library(ggvenn)
    library(VennDiagram)
    library(gplots)
    library(UpSetR)
    library(tidyverse)
    library(readxl)
```

Now, that the libraries are loaded, we are going to upload the input file in which we can find the connections between proteins and drugs:


```R    
    Dat <- read_excel("your_file_location.xlsx")
    names(Dat)[1]<- "X";  
    names(Dat)[2]<- "Y"; 
```

If you load the data correctly, the data frame looks like the following table, were each row is a connection between the two proteins in each column.


```R
    head(Dat, 5)
```
<img src=".\media\head01.png" style="width:400px;" />

The next step is to create the Graph that we are going to analyze, after you run this segment of code you will obtain an image like the following one.

```R
    library(igraph)
    g <- graph_from_data_frame(Dat, directed = FALSE)
    autograph(g)
```

<img src=".\media\Rplot1.png" style="width:600px;" />
 

Now, to obtain more information about the resulting graph, such as data that can be used to calculate some topological parameters like degree, centrality, betweenness, Pagerank, and closeness.

```R
    print(paste("The Graph has",
            length(degree(g)),
            "vertex",
            nrow(Dat),
            "edges, and",
            length(g),
            "connected components"))

    dg <- decompose.graph(g)

    for (i in 1:length(dg))
     { 
       cg <- dg[[i]]
       print(paste("Component", i, "Size:", length(degree(cg)) ) )
     }
```

Next we compute the following indices of each vertex, we will normalize our values, that means we will put all our values between 0 and 1.


### Degree
<div align="justify">In graph theory, the degree of a vertex of a graph is the number of edges that are incident to the vertex. In a biological network, the degree may indicate the regulatory relevance of the node. Proteins with very high degree are interacting with several other signaling proteins, thus suggesting a central regulatory role, that is they are likely to be regulatory hubs. The degree could indicate a central role in amplification (kinases), diversification and turnover (small GTPases), signaling module assembly (docking proteins), gene expression (transcription factors), etc. (Scardoni et al. 2009).</div>

```R
    Vertex <- as.data.frame(degree(g))
    Vertex$Degree <- normalize(as.numeric(Vertex$`degree(g)`))
    Vertex$`degree(g)` <- NULL
```    

### Centrality
<div align="justify">Centrality or eigenvector centrality (also called prestige score) is a measure of the influence of a node in a network. Relative scores are assigned to all nodes in the network based on the concept that connections to high-scoring nodes contribute more to the score of the node in question than equal connections to low-scoring nodes. A high eigenvector score means that a node is connected to many nodes who themselves have high scores.</div>


If **A** is the adjacency matrix of the graph **G** the relative centrality, <img src="https://render.githubusercontent.com/render/math?math=%24x_v%24">, score of vertex **v** can be defined as:
      
<img src="https://render.githubusercontent.com/render/math?math=%24%0Ax_v%20%3D%20%5Cfrac%7B1%7D%7B%5Clambda%7D%5Csum_%7Bt%5Cin%20M(v)%7Dx_t.%20%0A%24"  style="width:150px;" />

where **M(v)** is a set of the neighbors of **v** and <img src="https://render.githubusercontent.com/render/math?math=%24%5Clambda%24"> is a constant, in terms of the adjacency matrix this is <img src="https://render.githubusercontent.com/render/math?math=%24Ax%3D%5Clambda%20x%24">.

```R
    Vertex$Centrality <- eigen_centrality(g)$vector
```

### Betweenness


<div align="justify">The betweenness centrality (or "betweenness”) is a measure of centrality, for each vertex the betweenness is by definition the number of these shortest paths that pass through the vertex. For every pair of vertices in a connected graph, there exists at least one shortest path between the vertices such that the number of edges that the path passes through is minimized. Betweenness Centrality of a node in a protein signaling network, can indicate the relevance of a protein as functionally capable of holding together communicating proteins. The higher the value the higher the relevance of the protein as organizing regulatory molecules. Centrality of a protein indicates the capability of a protein to bring in communication distant proteins. In signaling modules, proteins with high Centrality are likely crucial to maintain the network’s functionality and coherence of signaling mechanisms (Scardoni et al. 2009). The betweenness  centrality <img src="https://render.githubusercontent.com/render/math?math=%24b(v)%24"> of a node v is defined by:</div>

<img src="https://render.githubusercontent.com/render/math?math=%24%0Ab(v)%20%3D%20%5Csum_%7Bs%5Cne%20v%5Cne%20t%5Cin%20V%7D%5Cfrac%7B%5Csigma_%7Bst%7D(v)%7D%7B%5Csigma_%7Bst%7D%7D%0A%24"   style="width:150px;" />

Where <img src="https://render.githubusercontent.com/render/math?math=%24%5Csigma_%7Bst%7D%24"> is the total number of shortest paths from node **s** to node **t** and <img src="https://render.githubusercontent.com/render/math?math=%24%5Csigma_%7Bst%7D(v)%24"> is the number of those paths that pass through **v**.

```R
    Vertex$Betweenness <- normalize(betweenness(g, normalized = TRUE ))
```    

### Pagerank


<div align="justify">PageRank is an algorithm used by Google Search to rank web pages, it is a way of measuring the importance of website pages. According to Google: “PageRank works by counting the number and quality of links to a page to determine a rough estimate of how important the website is. The underlying assumption is that more important websites are likely to receive more links from other websites.” Page-rank allows an immediate evaluation of the regulatory relevance of the node. A protein with a very high Page-rank is a protein interacting with several important proteins, thus suggesting a central regulatory role. A protein with low Page-rank, can be considered a peripheral protein, interacting with few and not central proteins (Scardoni et al. 2009).</div>

```R
    Vertex$PageRank <- normalize(page_rank(g)$vector)
```

### Closeness


<div align="justify">Closeness centrality (or closeness) of a node is a measure of centrality in a network, calculated as the reciprocal of the sum of the length of the shortest paths between the node and all other nodes in the graph. A protein with high closeness, compared to the average closeness of the network, will be central to the regulation of other proteins but with some proteins not influenced by its activity. A signaling network with a very high average closeness is more likely to be organized in functional units or modules, whereas a signaling network with very low average closeness will behave more likely as an open cluster of proteins connecting different regulatory modules (Scardoni et al. 2009). The equation for closeness is:</div>

<img src="https://render.githubusercontent.com/render/math?math=%24%0AC(x)%20%3D%20%5Cfrac%7B1%7D%7B%5Csum_y%20d(x%2Cy)%7D%0A%24"   style="width:150px;" />

Where <img src="https://render.githubusercontent.com/render/math?math=%24d(x%2Cy)%24"> is the distance between the vertices **x,y**. A high closeness can be thought of as an easy access to all nodes. This warning will appear but it would not affect the code: 
   "Warning message:
    In closeness(g) :
    At centrality.c:2874 :closeness centrality is not well-defined for disconnected graphs"
 
```R
    Vertex$Closeness <- normalize(closeness(g))
    
```


<div align="justify">Next we classify the vertex with values over the 50% for Degree, centrality, Betweenness and PageRank, and the top 1% for Closeness (because this parameter had a great number of top proteins using a 50% threshold). then we save a copy of the original vertex.</div>

```R
    Vertex$N <- c(1:length(Vertex$Degree))
    Vertex$DegreeCat <- ifelse(Vertex$Degree < 0.5, "no", "yes")
    Vertex$CentralityCat <- ifelse(Vertex$Centrality < 0.5, "no", "yes")
    Vertex$BetweennessCat <- ifelse(Vertex$Betweenness < 0.5, "no", "yes")
    Vertex$PageRankCat <- ifelse(Vertex$PageRank < 0.5, "no", "yes")
    Vertex$ClosenessCat <- ifelse(Vertex$Closeness < 0.99, "no", "yes")
    V_Original <- Vertex


    Best_Degree <- as.list(as.character(row.names(Vertex[Vertex$DegreeCat == "yes",])))
    Best_Closeness <- as.list(as.character(row.names(Vertex[Vertex$ClosenessCat == "yes",])))
    Best_Centrality <- as.list(as.character(row.names(Vertex[Vertex$CentralityCat == "yes",])))
    Best_Betweenness <- as.list(as.character(row.names(Vertex[Vertex$BetweennessCat == "yes",])))
    Best_PageRank <- as.list(as.character(row.names(Vertex[Vertex$PageRankCat == "yes",])))
```

The head of the final table for our vertex will appear with this command:

```R
    head(Vertex, 5)
```
<img src=".\media\image.png" style="width:400px;" />

Let's see the behavior of all the topological indexes that we have

```R
    Vertex <- Vertex[order(Vertex$Degree, decreasing = FALSE), ]
    Vertex$N <- c(1:nrow(Vertex) )
    df <- Vertex %>%
      select(N, Degree, Betweenness, Centrality, PageRank, Closeness) %>%
      gather(key = "variable", value = "value", -N)

    ggplot(df, aes(x = N, y = value)) + 
      geom_point(aes(color = variable), size=0.5)  +
      labs(title="All variables")
```

<img src=".\media\Rplot2.png" style="width:400px;" />



### Set Theory and Venn Diagrams.
We start by creating sets with the top 50% in each topological parameter, and then we will look for the intersections between parameters.


```R
      x <- list(
         Closeness = Best_Closeness, 
         Degree = Best_Degree,
         Centrality = Best_Centrality,
         Betweenness = Best_Betweenness,
         PageRank = Best_PageRank
        )
    
     display_venn <- function(x, ...){  
      grid.newpage()
      venn_object <- venn.diagram(x, filename = NULL, ...)
      grid.draw(venn_object)
       }
    display_venn(
      x,
      fill = c("#999999", "#E69F00", "#56B4E9", "#469F00", "#E09E75"),
    # Set names
    cat.cex = 1,
    cat.fontface = "bold",
    cat.default.pos = "outer",
    cat.dist = c(0.05, 0.08, 0.08, 0.06, 0.08)
    )
isect <- attr(venn(x, intersection=TRUE), "intersection")
```

<img src=".\media\Rplot30.png" style="width:400px;" />


Next we will see the size of the intersections in a bar diagram


```R
     input <- c(
     Centrality = length(isect$Centrality),
     #  Degree =length(isect$Degree),
     PageRank = length(isect$PageRank),
     # Closeness =length(isect$Closeness), 
     Betweenness =length(isect$Betweenness),
     # "Degree&Centrality" =  length(isect$`Degree:Centrality`),
     "Degree&PageRank" =  length(isect$`Degree:PageRank`),
     "Degree&Closeness" =  length(isect$`Closeness:Degree`),
     "Degree&Betweenness" =  length(isect$`Degree:Betweenness`),
     "Centrality&PageRank" =  length(isect$`PageRank:Centrality`),
     "Centrality&Closeness" =  length(isect$`Closeness:Centrality`),
     "Centrality&Betweenness" =  length(isect$`Betweenness:Centrality`),
     "PageRank&Closeness" =  length(isect$`Closeness:PageRank`),
     "PageRank&Betweenness" =  length(isect$`Betweenness:PageRank`),
     "Betweenness&Closeness" =  length(isect$`Closeness:Betweenness`),
     "Degree&Centrality&PageRank" =  length(isect$`Degree:Centrality:PageRank`),
     "Degree&Centrality&Closeness" =  length(isect$`Closeness:Degree:Centrality`),
     "Degree&Centrality&Betweenness" =  length(isect$`Degree:Centrality:Betweenness`),
     "Degree&PageRank&Closeness" =  length(isect$`Closeness:Degree:PageRank`),
     "Degree&PageRank&Betweenness" =  length(isect$`Degree:Betweenness:PageRank`),
     "Degree&Closeness&Betweenness" =  length(isect$`Degree:Closeness:Betweenness`),
     "Centrality&PageRank&Closeness" =  length(isect$`PageRank:Centrality:Closeness`),
     "Centrality&PageRank&Betweenness" =  length(isect$`PageRank:Centrality:Betweenness`),
     "Centrality&Closeness&Betweenness" =  length(isect$`Closeness:Centrality:Betweenness`),
     "PageRank&Closeness&Betweenness" =  length(isect$`Closeness:Betweenness:PageRank`),
     "Degree&Centrality&PageRank&Closeness" =  length(isect$`Closeness:Degree:Centrality:PageRank`), 
     "Degree&Centrality&PageRank&Betweenness" =  length(isect$`Degree:Centrality:Betweenness:PageRank`),
     "Centrality&PageRank&Betweenness&Closeness" =  length(isect$`Centrality:PageRank:Betweenness:Closeness`),
     "Degree&PageRank&Betweenness&Closeness" =  length(isect$`Closeness:Degree:Betweenness:PageRank`),
     #  "Degree&Centrality&Betweenness&Closeness" =  length(isect$`Closeness:Degree:Centrality:Betweenness`),
     "Degree&Centrality&PageRank&Betweenness&Closeness" =  length(isect$`Closeness:Degree:Centrality:Betweenness:PageRank`)
    )
     upset(fromExpression(input))
     
     print(isect)
```

<img src=".\media\Rplot-is.png" style="width:400px;" />

## Cut Analysis

<div align="justify">With this analysis we want to identify those proteins which have a key role in network connection given their location and first neighbour proteins. The cut analysis will allow to identify the proteins which generate at least 2 new components in the network when they are removed. Using this fragment of code we will generate a list of those proteins that disconnect the main graph, and the number of components that its elimination would generate in the network.</div> 

```R
    g1 <- graph_from_data_frame(Dat, directed = FALSE)
    dg <- decompose.graph(g1)
    g <- dg[[1]]
    cohesion(g)
    lista = c()
    for ( v in V(g)$name )
    {
      g1_new <- delete_vertices(g, v)
      if ( length(decompose.graph(g1_new)) > 1 ){
        print( paste(cohesion(g1_new), length(decompose.graph(g1_new)),v) )
        lista <- append(lista, v)
      }
      #print(v)
    }
    lista
    length(lista)
```

Using our dataset, this last fragment of code results in 240 nodes which disconnect the graph.

## References
+ Scardoni G, Laudanna C, Tosadori G, Fabbri F, Faizaan M. (2009) Analyzing biological network parameters with CentiScaPe.  Bioinformatics. doi:10.1093/bioinformatics/btp517

