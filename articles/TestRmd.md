# Add Citations to an RMarkdown Document and Print Bibliography

This is an R Markdown document. This is an example of a citation in the
text [Loh (1992)](#bib-loh). Now we cite in parentheses (e.g., [Baez and
Lauda, 2004b](https://arxiv.org/abs/math/0307200v3)). Notice the useful
‘b’ beside the year in the citation. You can change the default options
in a setup chunk at the start of the document or at any other point
using the `BibOptions` function or by specifying options as a list in
the `.opts` argument to the cite functions. In this example we mix
`"authoyear"` citation style with `"numeric"` bibliography style.

Note that I do not only have to cite by key, and may use all the
features of the `SearchBib` function to index into the BibEntry object.
Here are all the entries of type `Report` in my bibliography [Chiu and
Chow (1978)](#bib-chiu); [Padhye, Firoiu, and Towsley
(1999)](#bib-padhye). The hyperlinks will take you to their entry in the
bibliography. The link for [Markey
(2005)](http://tug.ctan.org/tex-archive/info/bibtex/tamethebeast/ttb_en.pdf)
will open the document in a new window; this is the default behaviour,
if a link is available (see
[`?open.BibEntry`](https://docs.ropensci.org/RefManageR/reference/open.BibEntry.md)).
The following citation has no hyperlink (de Geer, 1985). You can also
embed plots, to make the page longer:

``` r

plot(cars)
```

![](TestRmd_files/figure-html/unnamed-chunk-1-1.png) I’ve added a
reference to CTAN without citing it using the `NoCite` function. Now I’m
adding a reference from another bibliography (a second `BibEntry`
object) ([Serban, Staicu, and Carroll,
2013](#bib-serban2013multilevel)). Look at all my Aristotle: [Aristotle
(1907)](#bib-aristotleanima); [Aristotle (1929)](#bib-aristotlephysics);
[Aristotle (1968)](#bib-aristotlepoetics); [Aristotle
(1877)](#bib-aristotlerhetoric).

``` r

plot(cars)
```

![](TestRmd_files/figure-html/unnamed-chunk-2-1.png)

Some papers on the arXiv are [Baez and Lauda
(2004a)](https://arxiv.org/abs/math/0307200v3); [Baez and Lauda
(2004b)](https://arxiv.org/abs/math/0307200v3); [Itzhaki
(1996)](https://arxiv.org/abs/hep-th/9603067); [Wassenberg and Sanders
(2010)](https://arxiv.org/abs/1008.2849v1).

**References**

[\[1\]](#cite-aristotlerhetoric) Aristotle. *The Rhetoric of Aristotle
with a commentary by the late Edward Meredith Cope*. Ed. by E. M. Cope.
With a comment. by E. M. Cope. Vol. 3. 3 vols. Cambridge University
Press, 1877.

[\[2\]](#cite-aristotleanima) Aristotle. *De Anima*. Ed. by R. D. Hicks.
Cambridge: Cambridge University Press, 1907.

[\[3\]](#cite-aristotlephysics) Aristotle. *Physics*. Trans. by P. H.
Wicksteed and F. M. Cornford. New York: G. P. Putnam, 1929.

[\[4\]](#cite-aristotlepoetics) Aristotle. *Poetics*. Ed. by D. W.
Lucas. Clarendon Aristotle. Oxford: Clarendon Press, 1968.

[\[5\]](#cite-chiu) W. W. Chiu and W. M. Chow. *A Hybrid Hierarchical
Model of a Multiple Virtual Storage (MVS) Operating System*. Research
rep. RC-6947. IBM, 1978.

\[6\] I. de Geer. “Earl, Saint, Bishop, Skald~- and Music. The Orkney
Earldom of the Twelfth Century. A Musicological Study”. PhD thesis.
Uppsala: Uppsala Universitet, 1985.

[\[7\]](#cite-loh) N. C. Loh. “High-Resolution Micromachined
Interferometric Accelerometer”. MA Thesis. Cambridge, Mass.:
Massachusetts Institute of Technology, 1992.

[\[8\]](#cite-itzhaki) N. Itzhaki. *Some remarks on ’t Hooft’s S-matrix
for black holes*. Mar. 11, 1996. arXiv:
[hep-th/9603067](https://arxiv.org/abs/hep-th/9603067).

[\[9\]](#cite-padhye) J. Padhye, V. Firoiu, and D. Towsley. *A
Stochastic Model of TCP Reno Congestion Avoidance and Control*. Tech.
rep. 99-02. Amherst, Mass.: University of Massachusetts, 1999.

[\[10\]](#cite-baezarticle) J. C. Baez and A. D. Lauda.
“Higher-Dimensional Algebra V: 2-Groups”. Version 3. In: *Theory and
Applications of Categories* 12 (2004), pp. 423-491. arXiv:
[math/0307200v3](https://arxiv.org/abs/math/0307200v3).

[\[11\]](#cite-baezonline) J. C. Baez and A. D. Lauda.
*Higher-Dimensional Algebra V: 2-Groups*. Oct. 27, 2004. arXiv:
[math/0307200v3](https://arxiv.org/abs/math/0307200v3).

[\[12\]](#cite-markey) N. Markey. *Tame the BeaST. The B to X of
BibTeX*. Oct. 16, 2005. URL:
<http://tug.ctan.org/tex-archive/info/bibtex/tamethebeast/ttb_en.pdf>
(visited on 10/01/2006).

[\[13\]](#cite-ctan) *CTAN. The Comprehensive TeX Archive Network*.
2006. URL: <https://www.ctan.org> (visited on 10/01/2006).

[\[14\]](#cite-wassenberg) J. Wassenberg and P. Sanders. *Faster Radix
Sort via Virtual Memory and Write-Combining*. Aug. 17, 2010. arXiv:
[1008.2849v1 \[cs.DS\]](https://arxiv.org/abs/1008.2849v1).

**More References**

[\[1\]](#cite-serban2013multilevel) N. Serban, A. M. Staicu, and R. J.
Carroll. “Multilevel Cross-Dependent Binary Longitudinal Data”. In:
*Biometrics* 69.4 (2013), pp. 903-913.
