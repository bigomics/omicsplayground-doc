.. _GeneSets:

GeneSets
================================================================================

This module is subdivided into four submodules: **Geneset enrichment**, 
**Test Geneset**, **Pathway Analysis** and **Word cloud**.


Geneset enrichment
--------------------------------------------------------------------------------
Similar to the differential gene expression analysis, users can perform differential
expression analysis on a geneset level in this page, which is also referred as 
gene set enrichment (GSE) analysis. The platform has more than 50.000 genesets 
(or pathways) in total that are divided more than 30 geneset collections such 
`Hallmark <https://www.cell.com/abstract/S0092-8674(11)00127-9>`__, 
`Reactome <https://reactome.org/>`__,
`Wikipathways <https://www.wikipathways.org/>`__, 
and Gene Ontology (`GO <http://geneontology.org/>`__).
Users have to specify which comparison they want to visually analyze 
employing a certain geneset collection.

The tab consists of the settings panels as well as four results panels: **Top enriched gene sets**, 
**Frequency in top gene sets**, a **Table** panel where users can swicth between three tables and **Genes in gene sets**.


Settings panel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The enrichment analysis can be started by selecting a contrats of interest in 
the ``Contrast`` and specifying a relevent gene set family in the ``Gene set collection``.
It is possible to set the false discovery rate (FDR) and the logarithmic fold change 
(logFC) thresholds under the ``FDR`` and ``logFC threshold`` settings, respectively.
We allow users to show all gene sets in the``Enrichment analysis`` table , rather than just the significant ones, under the *Options* menu.
Users can also select statistical methods for the enrichment analysis from the same menu.
To ensure the statistical reliability, the platform performs enrichment analyses using multiple methods, including 
`Spearman rank correlation <https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient>`__, 
`GSVA <https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-14-7>`__, 
`ssGSEA <https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-14-7>`__, 
`Fisher's exact test <https://www.jstor.org/stable/2340521?seq=1#metadata_info_tab_contents>`__, 
`GSEA <http://software.broadinstitute.org/gsea/index.jsp>`__, 
`camera <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3458527/>`__ and 
`fry <https://academic.oup.com/bioinformatics/article/26/17/2176/200022>`__. Finally users can limit the results to only the top 10 
up- and down-regulated gene sets.

.. figure:: figures_v3/GE_settings.png
    :align: center
    :width: 20%


Top enriched gene sets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This panel displays the enrichment plots of the top differentially enriched gene sets (up and down) for the selected contrast. 
Black vertical bars indicate the rank of genes in the gene set in the sorted list metric. 
The green curve corresponds to the enrichment score (ES). The more the green ES curve is shifted to the upper left of the graph, 
the more the gene set is enriched in the first group. Conversely, a shift of the ES curve to the lower right, 
corresponds to more enrichment in the second group. This panel will by default display the 12 most up-regulated genesets 
in the selected contrast. Selecting a specific gene set from the 'Enrichment analysis' table below it will display 
the selected gene set alone.


.. figure:: figures_v3/GE_enrichment_1.png
    :align: center
    :width: 100%


Frequency in top gene sets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This panel shows the number of times a gene is present in the top-N genesets sorted by frequency. Genes that are frequently shared among the top enriched gene sets may suggest driver genes.


.. figure:: figures_v3/GE_enrichment_2.png
    :align: center
    :width: 100%


The settings icon open the settings menu from which users can select the number of top gene sets to be used (``Number of top sets``), 
whether to weight by geneset size (``Weight by geneset size``) and whether to weight by fold-change (``Weight by FC``).

.. figure:: figures_v3/GE_freq_opts.png
    :align: center
    :width: 20%



Table
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This table shows the enrichment analysis results from the selected statistical methods.
With default settings, this table reports the meta (combined) results of 
`camera <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3458527/>`__,
`fgsea <http://software.broadinstitute.org/gsea/index.jsp>`__, and 
`Spearman rank correlation <https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient>`__ only.
Users can also display individual q-values for each of the selected analysis methods using the settings on top of the table.

.. figure:: figures_v3/GE_table_opts.png
    :align: center
    :width: 20%
    
The combined enrichment analysis results from the methods are displayed in this table,
where for each geneset the ``meta.q`` corresponds to the highest ``q`` value provided
by the methods and the number of ``stars`` indicate how many methods identified
the geneset as significant (``q < 0.05``). ``AveExpr0`` and ``AveEprx1`` refer to the average gene set expression 
in group 0 and group 1 of the selected pairwise comparison respectively.
The table is interactive; users can sort it by ``logFC``, ``meta.q``, ``AveExpr0``, ``AveEprx1`` and ``stars``.

.. figure:: figures_v3/GE_enrichment_3.png
    :align: center
    :width: 100%


Genes in gene set
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
By clicking on a gene set in the **Table** above, it is possible to see the gene list of 
that gene set under **Genes in gene set**. this table also reports the fold-change, statistics and 
correlation of the genes in the selected gene set. By clicking on a gene in this table, users can check 
the expression status of the gene for the selected contrast in the *Expression barplot* and its correlation to the gene set
in the *Enrichment vs. expression* scatter plot under the **Geneset expression** tab, discussed in the next section.


.. figure:: figures_v3/GE_enrichment_4.png
    :align: center
    :width: 100%



Geneset expression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The **Geneset expression** panel provide plots associated with the gene set 
selected in **Table** and gene selected in **Genes in gene set**, as explained in the previous section.

:**Volcano Plot**: Volcano-plot of genes showing the significance versus the fold-change on the y and x axes,
        respectively. Genes in the selected gene set are highlighted in blue.  
:**Enrichment barplot**: Enrichment plot associated with the gene set selected from **Table**. Samples in the barplot 
        can be ungrouped via the plot settings icon.
:**Expression barplot**: Barplot of the gene expression of the gene. Samples in the barplot 
        can be ungrouped via the plot settings icon.
:**Enrichment vs. expression**: Scatter plot of the enrichment versus the expression of the selected 
        geneset and gene, on the y and x axes, respectively.

.. figure:: figures_v3/GSEA_exp.png
    :align: center
    :width: 100%


Enrichment by comparison
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Under the **Enrichment by comparison** panel, users can fin enrichment plots for the selected gene
set (in **Table**) across multiple contrasts. The figure allows to quickly 
compare the enrichment of a certain gene set across all other comparisons.

.. figure:: figures_v3/GSEA_comp.png
    :align: center
    :width: 100%


Volcano by comparison
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The **Volcano by comparison** panel simultaneously displays volcano plots of gene sets 
enrichment across all contrasts, showing the enrichment score versus significance 
on the x and y axes, respectively. This provides users an overview of the 
statistics across all comparisons. By comparing multiple volcano plots, the user
can immediately see which comparison is statistically weak or strong.
Experimental contrasts showing better statistical significance will show volcano
plots with 'higher' wings.

.. figure:: figures_v3/GSEA_volc_comp.png
    :align: center
    :width: 100%


Volcano by method
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Under the **Volcano by method** panel, users can see the simultaneous 
visualisation of volcano plots of gene sets for different enrichment methods.
This provides users an quick overview of the sensitivity of the statistical 
methods at once. Methods showing better statistical significance will show 
volcano plots with 'higher' wings.

.. figure:: figures_v3/GSEA_volc_met.png
    :align: center
    :width: 100%


Enrichment (all)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 
The **Enrichment (all)** table provides the enrichment scores of gene sets 
across all contrasts. It is also possible to visualise all q-values 
from the setting icon on top of the plot. 

.. figure:: figures_v3/GE_enrichment_all.png
    :align: center
    :width: 100%


FDR table
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 
The **FDR table** panel reports the number of significant gene sets at different 
FDR thresholds for all contrasts and methods. Using the table the user can
determine which statistical methods perform better for a particular contrast.
The left part of the table (in blue) correspond 
to the number of significant down-regulated gene sets, the right part (in red) 
correspond to the number of significant overexpressed gene sets.

.. figure:: figures_v3/GE_enrichment_FDR.png
    :align: center
    :width: 100%


Test geneset
--------------------------------------------------------------------------------
The **Test geneset** submodule is used to test a specific user-defined geneset, or, alternatively, a geneset from 
the KEGG or Hallmark collection or a list of genes extracted from the available pairwise comparisons, for enrichment
in the experimental dataset. The plot contain five tabs: **Enrichment table**, **Volcano plots**, **Enrichment**, **Overlap/similarity** and **Markers**.


Settings panel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The settings panel of the **Test geneset** module consists of a box where users can paste gene lists to be queried.
Three examples of gene lists are provided below it, namely the *apoptosis*, *cell_cycle* and *immune_chkpt* lists.
Users can also select specific KEGG and hallmark gene sets from the *Options* in the panel, as well as using
the differentially expressed genes or proteins from one of the contrasts.

.. figure:: figures_v3/test_settings.png
    :align: center
    :width: 20%


Enrichment table
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This tab is shown indepently of the other four. It display two tables. The first table, *Enrichment by contrasts*, 
shows the enrichment scores of query signature across all contrasts. The table summarizes the enrichment statistics
of the gene list in all contrasts using the GSEA algorithm. The NES corresponds to the normalized enrichment score of the GSEA analysis.

.. figure:: figures_v3/test_ET.png
    :align: center
    :width: 100%

The second table, *Genes in signature*, is based on which pairiwse comparison is selected in *Enrichment by contrasts* and shows 
the genes of the current signature corresponding to the selected contrast. Genes are sorted by decreasing (absolute) fold-change.

.. figure:: figures_v3/test_gis.png
    :align: center
    :width: 100%

Volcano plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This tab contains volcano plots showing where the genes of a test signatures fall in the experimental pairiwse comparisons.
For positive enrichment, genes of the query signature would fall on the upper right of the volcano plot, for negative enrichment, on the upper left.


.. figure:: figures_v3/test_volc.png
    :align: center
    :width: 100%


Enrichment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In this tab, multiple plots show the enrichment of the query signature in all constrasts. Positive enrichment
means that a particular contrast shows similar expression changes as the query signature. Users can either view 
the plots of all teh contrasts, while selecting a specific contrast in the *Enrichment by contrasts* table will 
only display the ernichment plot for it.


.. figure:: figures_v3/test_enr.png
    :align: center
    :width: 100%

Overlap/similarity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Under the Overlap/similarity tab, users can find the similarity of their gene list with all the gene sets and pathways in the platform, including statistics such as the total number of genes in the gene set (K), the number of intersecting genes between the list and the gene set (k), the overlapping ratio of k/K, logarithm of the odds ratio (log.OR), as well as the p and q values by the Fisher’s test for the overlap test. 

The *Signature overlap scores* plot is located on top. Its vertical axis shows the overlap score of the gene set which combines the odds ratio and significance (q-value) of the Fisher's test. The*Overlap with other signatures* table is located below it and contain various statistical values.

.. figure:: figures_v3/test_overlap.png
    :align: center
    :width: 100%


The *Signature overlap scores* plot can also be customised via the settings icon, where users can select the number of signatures 
to display (``Number of features``) and can toggle the signature names on and off (``Show features names``).

.. figure:: figures_v3/test_overlap_opts.png
    :align: center
    :width: 20%

Markers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The **Markers** tab contains a series of plots (under *Markers plot*) showing the expression levels of the tested genes in the dataset samples as a colored t-SNE plot in red (highly expressed) and light grey (low expressed). The first figure shows the single-sample enrichment of your signature list in red (upregulation) and blue (downregulation).

.. figure:: figures_v3/test_markers.png
    :align: center
    :width: 100%


The plots can be sorted via the ``Sort by`` option in the settings icon by correlation (default), probability or name. ``Layout`` swaps the 
layout of the plots between a 4x4 (default) and a 6x6 grid.

.. figure:: figures_v3/test_markers_opts.png
    :align: center
    :width: 20%


Pathway analysis
--------------------------------------------------------------------------------
This module performs specialized enrichment analysis
providing higher level functional and visual interpretation.

The **WikiPathways** panel maps the differential fold-changes onto
the `WikiPathways <https://www.wikipathways.org/>`__
pathway maps. The **Reactome** panel does the same for the
`Reactome <https://reactome.org/>`__ pathway maps. Under the
**GO** panel, a graph-based enrichment
analysis is done using the Gene Ontology (`GO
<http://geneontology.org/>`__) graph structure.


Settings panel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Users can specify the contrast of their interest
in the ``Contrast`` settings. Under the main *Options*, users can
select ``filter significant (tables)``  to keep only significant entries in the table.

.. figure:: figures_v3/Pathway_settings.png
    :align: center
    :width: 20%


WikiPathways
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
`WikiPathways <https://www.wikipathways.org/>`__ is a public collection
of manually curated pathways representing the current knowledge of molecular 
interactions, reactions and relation networks as pathway maps. In the 
**WikiPathways** panel, each pathway is scored for the selected contrast profile
and reported in the table. An activation-heatmap comparing the activation levels of pathways across multiple
contrast profiles is generated. This facilitates the quick detect the similarities 
between profiles in certain pathways. More detailed explaination of each output
is provided below.

:**WikiPathway**: In the pathway map, genes are colored according to their upregulation 
        (red) or downregulation (blue) in the contrast profile. Each pathway 
        is scored for the selected contrast profile and reported in the table 
        below the plot.

:**Enrichment table**: The table is interactive; enabling user to sort on 
        different variables (WikiPathways id, pathway, logFC and meta q-values) 
        and select a pathway by clicking on the row in the table.

:**Activation matrix**: The activation matrix visualizes the activation levels of pathways
        (or pathway keywords) across multiple contrast profiles. This facilitates
        to quickly see and detect the similarities of certain pathways between
        contrasts. The size of the circles correspond to their relative activation,
        and are colored according to their upregulation (red) or downregulation
        (blue) in the contrast profile. The matrix can be normalised from the 
        *settings* icon.

.. figure:: figures_v3/Pathway_wiki.png
    :align: center
    :width: 100%


Reactome
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
`Reactome <https://reactome.org/>`__ is a collection
of manually curated pathways representing the current knowledge of molecular 
interactions, reactions and relation networks as pathway maps. In the 
**Reactome** panel, each pathway is scored for the selected contrast profile
and reported in the table. A unique feature of the platform is that it provides 
an activation-heatmap comparing the activation levels of pathways across multiple
contrast profiles. An activation-heatmap comparing the activation levels of pathways across multiple
contrast profiles is generated.  More detailed explaination of each output
is provided below.

:**Reactome**: In the pathway map, genes are colored according to their upregulation 
        (red) or downregulation (green) in the contrast profile. Each pathway 
        is scored for the selected contrast profile and reported in the table 
        below the plot.

:**Enrichment table**: The table is interactive; enabling user to sort on 
        different variables (Reactome id, pathway, logFC and meta q-values) 
        and select a pathway by clicking on the row in the table.

:**Activation matrix**: The activation matrix visualizes the activation levels of pathways
        (or pathway keywords) across multiple contrast profiles. This facilitates
        to quickly see and detect the similarities of certain pathways between
        contrasts. The size of the circles correspond to their relative activation,
        and are colored according to their upregulation (red) or downregulation
        (blue) in the contrast profile. The matrix can be normalised from the 
        *settings* icon.

.. figure:: figures_v3/Pathway_reactome.png
    :align: center
    :width: 100%


GO graph
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the **GO** panel, users can perform `GO <http://geneontology.org/>`__ analysis.
GO defines functional concepts/classes and their relationships as a hierarchical
graph. 
The GO database provides a computational representation of the current knowledge 
about roles of genes for many organisms in terms of molecular functions, cellular
components and biological processes. All the features described under the 
**KEGG pathway** panel, such as scoring the gene sets and drawing an 
activation-heatmap,
can be performed for the GO database under the GO graph tab. Instead of pathway
maps, an annotated graph structure provided by the GO database is potted for
every selected gene set. 
Each output chart/table of the panel is describer below in detail.

:**Gene Ontology graph**: The structure of GO can be described in terms of a graph, where each
        GO term is a node, and the relationships between the terms are edges 
        between the nodes. GO is loosely hierarchical, with 'child' terms being
        more specialized than their 'parent' terms. The graph is interactive. 
        You can move the graph and zoom in using the mouse.
        Under the graph *settings*, users can select ``Prune tree`` to prune
        the tree only with significant branches and ``color custers`` to 
        highlight clusters with different colors

        .. figure:: figures_v3/Pathway_GO_opts.png
            :align: center
            :width: 25%

:**GO score table**: The scoring of a GO term is performed by considering
        the cumulative score of all terms from that term to the root node. 
        That means that GO terms that are supported by higher level terms
        levels are preferentially scored.

:**Activation matrix**: The GO activation matrix visualizes the activation of GO terms
        across conditions. From this figure, you can easily detect GO terms
        that are consistently up/down across conditions. The size of the circles
        correspond to their relative activation, and are colored according to 
        their upregulation (red) or downregulation (blue) in the contrast
        profile. The matrix can be normalised from the *settings* icon.

.. figure:: figures_v3/Pathway_GO.png
    :align: center
    :width: 100%


Word Cloud
--------------------------------------------------------------------------------
The **WordCloud** panel performs "keyword enrichment analysis". It
computes enrichment of a selected keyword across all contrasts. Select
a keyword by clicking a word in the 'Enrichment table'. Keyword
enrichment is computed by running GSEA on the enrichment score profile
for all contrasts. We defined the test set as the collection of
genesets that contain the keyword in the title/description.


Settings panel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Users can specify the contrast of their interest
in the ``Contrast`` settings.

.. figure:: figures_v3/WC_settings.png
    :align: center
    :width: 20%
              

Main panel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The main panel consists of five different outputs:
        
:**Enrichment plots**: The plots visualize the enrichment of the
    selected keyword in the contrasts.  Black vertical bars
    indicate the position of gene sets that contains the *keyword*
    in the ranked list of enrichment scores. The curve in green
    corresponds to the 'running statistic' of the keyword
    enrichment score. The more the green ES curve is shifted to
    the upper left of the graph, the more the keyword is enriched
    in the first group. Conversely, a shift of the green ES curve
    to the lower right, corresponds to keyword enrichment in the
    second group.

:**Word cloud**: The word cloud plot visualizes the frequency/enrichment of
    keywords for the data set. Select a keyword in the 'Enrichment
    table'. In the plot settings, users can exclude certain words
    from the figure, or choose the color palette. The sizes of the
    words are relative to the normalized enrichment score (NES)
    from the GSEA computation. Keyword enrichment is computed by
    running GSEA on the mean (squared) enrichment profile
    (averaged over all contrasts). For each keyword, we defined
    the 'keyword set' as the collection of genesets that contain
    that keyword in the title/description.

        .. figure:: figures_v3/WC_wc_opts.png
            :align: center
            :width: 25%

:**Word t-SNE**: The Word t-SNE plot visualizes the similarity of the
    keywords that were found in the title/description of gene
    sets. Keywords that are often found together in
    title/descriptions are placed close together in the t-SNE. For
    each keyword we computed enrichment using GSEA on the mean
    (absolute) enrichment profiles (averaged over all
    contrasts). Statistically significant gene sets (q<0.05) are
    colored in red. The sizes of the nodes are proportional to the
    normalized enrichment score (NES) of the keyword. In the plot
    settings, the user can choose between t-SNE and "Uniform
    Manifold Approximation and Projection" (UMAP).

        .. figure:: figures_v3/WC_tsne_opts.png
            :align: center
            :width: 25%

:**Enrichment table**: The Enrichment table summarizes the results from the
    enrichment test for the tested keywords. The NES corresponds
    to the normalized enrichment score from the GSEA analysis.

:**Leading-edge table**: The Leading-edge table shows the geneset titles that have
    contributed to the enrichment of the selected keyword.

.. figure:: figures_v3/WC_main.png
    :align: center
    :width: 100%
