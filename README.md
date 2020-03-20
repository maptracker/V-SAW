### V-SAW - Virology Sequence Analysis Workbench

_The code for this tool is unpublished, primarily because it involved
too many BMS-internal connections to cleanly extract it for
disclosure, but also because its function (identification of
population variants in Sanger sequences) is now almost certainly
better done via NGS. Its operation was interesting enough to note
however, hence this small place-holder repo._

V-SAW supported our hepatitis C virus (HCV) program. HCV is infamous
for being highly mutable, such that drug treatment - even with a
multi-drug cocktail - was challenging because the virus would
"respond" to the selective pressure applied by the drug and mutate to
a novel, drug-resistant form. As such, the program needed a mechanism
to monitor the genomes of the viral population in patients undergoing
treatment, in order to highlight mutations that might be arising "in
response to" the drug.

[Mingyi Liu][Mingyi] wrote an incredible front end for
V-SAW. [Carlos Rios][Carlos] wrote the database that held the
company's Sanger sequence. My work centered on the analysis of the raw
sequence trace files to identify polymorphic sites in a patient's
viral load.

What was available at the time was [Sanger sequnce][Sanger] of viral
genomic sequence amplified directly from patient blood plasma. As
such, these sequences represented population sequence from millions of
virions. Conserved bases would appear as "normal" peaks in the trace,
while locations that had two or more bases significantly represented
would show two or more peaks. These "Mixed" locations represented loci
that were potentially undergoing selective mutation.

My code utilized peak boundaries defined by [Phred][Phred] to analyze
peak heights within each base. It took into account local noise levels
in an attempt to highlight locations that appeared to have two or more
significant bases present. After submitting new sequences to the tool,
researchers would then validate each location. The validation tool was
designed for speed and clarity in order to facilitate an otherwise
tedious review of hundreds of loci. Each validation was recorded under
the researcher's user ID, and two or more researchers reviewed each
sample. Loci that were inconsistent (marked as Mixed by one researcher
but NotMixed by another) could also be easily pulled up for further
review.

![V-SAW Workflow][Workflow]

My contribution was in the yellow boxes above. My code would
ultimately generate JSON structures that would be read by Mingyi's
viewer.

* [BMS Public Disclosure approval](PubD-Disclosure-Approval.md)

[Mingyi]: http://mingyi.org/
[Carlos]: https://www.linkedin.com/in/carlos-b-rios-b7861b30
[Sanger]: https://en.wikipedia.org/wiki/Sanger_sequencing
[Phred]: https://en.wikipedia.org/wiki/Phred_base_calling

[Workflow]: img/V-SAW_Workflow.png
