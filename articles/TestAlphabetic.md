# Add Citations to an RMarkdown Document and Print Bibliography

``` r

library(RefManageR)
bib <- ReadBib(system.file("Bib", "biblatexExamples.bib", 
                           package = "RefManageR"), check = FALSE)
BibOptions(check.entries = FALSE, style = "markdown", bib.style = "alphabetic", cite.style = 'alphabetic')
```

This is an R Markdown document. This is an example of a citation in the
text [Herrmann, Öfele, Schneider et al. \[Her+06\]](#bib-herrmann). Now
we cite in parentheses \[e.g.,
[BL04](https://arxiv.org/abs/math/0307200v3)\]. You can change the
default options in a setup chunk at the start of the document or at any
other point using the `BibOptions` function or by specifying options as
a list in the `.opts` argument to the cite functions.

These are reports [Chiu and Chow \[CC78\]](#bib-chiu); [Padhye, Firoiu,
and Towsley \[PFT99\]](#bib-padhye). Their hyperlinks go to their entry
in the bibliography. The link for
\[[Mar05](http://tug.ctan.org/tex-archive/info/bibtex/tamethebeast/ttb_en.pdf)\]
will take you to the document in a new window; this is the default
behaviour, if a link is available (see
[`?open.BibEntry`](https://docs.ropensci.org/RefManageR/reference/open.BibEntry.md)).
The following citation has no hyperlink \[Gee85\]. You can also embed
plots, for example:

``` r

plot(cars)
```

![](TestAlphabetic_files/figure-html/unnamed-chunk-1-1.png) I’ve added a
reference to CTAN without citing it. Look at all my Aristotle:
\[[Ari07](#bib-aristotleanima); [Ari29](#bib-aristotlephysics);
[Ari68](#bib-aristotlepoetics); [Ari77](#bib-aristotlerhetoric)\].

``` r

plot(cars)
```

![](TestAlphabetic_files/figure-html/unnamed-chunk-2-1.png)

Some papers on the arXiv are [Baez and Lauda
\[BL04\]](https://arxiv.org/abs/math/0307200v3); [Baez and Lauda
\[BL04\]](https://arxiv.org/abs/math/0307200v3); [Itzhaki
\[Itz96\]](https://arxiv.org/abs/hep-th/9603067); [Wassenberg and
Sanders \[WS10\]](https://arxiv.org/abs/1008.2849v1).

**References**

[\[Ari07\]](#cite-aristotleanima) Aristotle. *De Anima*. Ed. by R. D.
Hicks. Cambridge: Cambridge University Press, 1907.

[\[Ari29\]](#cite-aristotlephysics) Aristotle. *Physics*. Trans. by P.
H. Wicksteed and F. M. Cornford. New York: G. P. Putnam, 1929.

[\[Ari68\]](#cite-aristotlepoetics) Aristotle. *Poetics*. Ed. by D. W.
Lucas. Clarendon Aristotle. Oxford: Clarendon Press, 1968.

[\[Ari77\]](#cite-aristotlerhetoric) Aristotle. *The Rhetoric of
Aristotle with a commentary by the late Edward Meredith Cope*. Ed. by E.
M. Cope. With a comment. by E. M. Cope. Vol. 3. 3 vols. Cambridge
University Press, 1877.

[\[BL04\]](#cite-baezarticle) J. C. Baez and A. D. Lauda.
“Higher-Dimensional Algebra V: 2-Groups”. Version 3. In: *Theory and
Applications of Categories* 12 (2004), pp. 423-491. arXiv:
[math/0307200v3](https://arxiv.org/abs/math/0307200v3).

[\[BL04\]](#cite-baezonline) J. C. Baez and A. D. Lauda.
*Higher-Dimensional Algebra V: 2-Groups*. Oct. 27, 2004. arXiv:
[math/0307200v3](https://arxiv.org/abs/math/0307200v3).

[\[CC78\]](#cite-chiu) W. W. Chiu and W. M. Chow. *A Hybrid Hierarchical
Model of a Multiple Virtual Storage (MVS) Operating System*. Research
rep. RC-6947. IBM, 1978.

[\[CTAN06\]](#cite-ctan) *CTAN. The Comprehensive TeX Archive Network*.
2006. URL: <https://www.ctan.org> (visited on 10/01/2006).

\[Gee85\] I. de Geer. “Earl, Saint, Bishop, Skald~- and Music. The
Orkney Earldom of the Twelfth Century. A Musicological Study”. PhD
thesis. Uppsala: Uppsala Universitet, 1985.

[\[Her+06\]](#cite-herrmann) W. A. Herrmann, K. Öfele, S. K. Schneider,
et al. “A carbocyclic carbene as an efficient catalyst ligand for C-C
coupling reactions”. In: *Angew.~Chem. Int.~Ed.* 45.23 (2006),
pp. 3859-3862.

[\[Itz96\]](#cite-itzhaki) N. Itzhaki. *Some remarks on ’t Hooft’s
S-matrix for black holes*. Mar. 11, 1996. arXiv:
[hep-th/9603067](https://arxiv.org/abs/hep-th/9603067).

[\[Mar05\]](#cite-markey) N. Markey. *Tame the BeaST. The B to X of
BibTeX*. Oct. 16, 2005. URL:
<http://tug.ctan.org/tex-archive/info/bibtex/tamethebeast/ttb_en.pdf>
(visited on 10/01/2006).

[\[PFT99\]](#cite-padhye) J. Padhye, V. Firoiu, and D. Towsley. *A
Stochastic Model of TCP Reno Congestion Avoidance and Control*. Tech.
rep. 99-02. Amherst, Mass.: University of Massachusetts, 1999.

[\[WS10\]](#cite-wassenberg) J. Wassenberg and P. Sanders. *Faster Radix
Sort via Virtual Memory and Write-Combining*. Aug. 17, 2010. arXiv:
[1008.2849v1 \[cs.DS\]](https://arxiv.org/abs/1008.2849v1).
