The description for the interval/points ontologies (free for academic- non commercial use-please cite source if used):
 
temporal points:
You will need to install Protege 4.3 (versions 4.x support OWL 2.0,
which is the current standard, previous versions such as 3.x don't)
from:

http://protege.stanford.edu/

Then you must be able to see SWRL rules into ontologies so at Protege
menu click:
window->Views->Ontology views-> Rules.

Then you can start checking the files, in fact they
are not ontologies, they contain just the class Points (time points),
object properties between points (before,after,equals defining the
ordering of points)  and in some of these files there is the datatype
property time specifying a point using the date. All files contain
some examples (individuals) to check them.
So files:
a) quantitative.owl contains Points and rules that specify their
ordering (before,after etc) by comparing their dates (data property)
using SWRL rules. The only reasoner currently supporting datatype
comparisons in SWRL is Pellet so if you check at Reasoners->Pellet and
then start reasoner, you will notice that for each individual
of class Point (p1,p2,p3) the relation with other points is inferred.
If you try the same thing with HermiT or Fact++ then nothing appears.
b) Qualitative-swrl.owl : again Points but only the properties
before/after/equals are used, no data property for dates. For each
point the relation (before/equals) with the previous one is asserted
and then reasoning rules in SWRL infer additional relations. Currently
Pellet and HermiT support SWRL (HermiT only with rules without
datatypes) so you can do reasoning with one of these two.
c) qualitative-ri-axioms.owl : again only object properties
before/after/equals and no dates. But instead of infering temporal
relations using SWRL, OWL subproperty axioms (or Role Inclusion Axioms
RI-axioms) are used. You can see these axioms if you click on the
object property before, at bottom left of protege window. In fact
these axioms do the same job as SWRL rules of the previous ontology.
Role Inclusion axioms are only supported by OWL 2 (that's why you need
Protege 4.x) but all OWL 2 compatible reasoners support them so you
can do reasoning with Pellet, HermiT and Fact++.
d) combined-q.owl : this is the result of combining ontologies  (a)
and (b), so you can assert both dates and object properties and do
reasoning with SWRL rules both for dates and for object properties
before/after/equals. These 3 object properties are called qualitative
because you can do reasoning with points without knowing numerical
(quantitative) values such as dates. Since SWRL rules with datatypes
are included only Pellet can be used for reasoning with this.
e) combined-axioms.owl : same as (d) but in this case (a) is combined
with (c) for supporting both quantitative and qualitative defined
points. Again only Pellet can be used at the moment.
intervals:
a) qualitative-Allen.owl : here we work using directly qualitative (no
dates, times) relations of intervals and reasoning over them using
SWRL. Also no points are used, interval relations directly. These
relations (object properties) are the Allen relations:
http://www.ics.uci.edu/~alspaugh/cls/shr/allen.html
In the ontology i use a for after, b for before, d for during,di for
contains (inverse of during), o for overlaps, oi overlapped by, f
finishes, fi finished by, s starts, si started by, m for meet, mi for
met by and eq for equals. 13 basic relations and some additional ones
(those with the underscore) used for reasoning. Reasoning is achieved
using SWRL, both HermiT and Pellet can be used. Notice that this is a
very complex representation involving hundreds of rules.

b) time-quantitative-only.owl This is basically the opposite of the
previous one: there are classes ProperIntervals (for intervals) and
Instants (for Points) which are subclasses of temporal entity. Each
ProperInterval is related with two Instants (points) with object
properties hasBeginning and hasEnd. Each Instant in turn has a data
property inXSDDateTime that specifies the date and time for it. Then
all interval relations (object properties) are extracted by comparing
the dates of beginnings and endings of all intervals using SWRL rules.
Only Pellet can be used, and dates are needed for all points.

c) time-qualitative-only.owl : Similar to (b) again ProperIntervals
related with Instants that are their beginning and ending points. The
difference is that Instants don't have dates but instead their
relation (before/after) with previous/next Instant is asserted.
Reasoners extract interval relations using SWRL rules. Since no
datetimes are involved HermiT can be used in addition to Pellet.

d) time-combined-swrl.owl : this is the result of combining (b) and
(c) so again intervals and points but you can assert both datetime of
points or before/after relation with other points. So both
quantitative and qualitative relations are supported. Reasoning with
Pellet.

e) and another one interval representation (file
time-quantitative-direct-intervals.owl)
Similar to case (b) of forwarded message but instead of associating
each interval with two points and attach dates to points, each
interval is associated directly with two dates (startValue and
endValue-check example individuals) ,that may make reasoning faster.
Reasoning only with Pellet.
So in total 5 alternative representations for points and 5 for intervals.

Spatial Representations:
a) RCC5-Qualitative and RCC8-qualitative: RCC topological relations using qualitative representation.
   Reasoning using HermiT and Pellet.
b) RCC5-coordinates and RCC8-coordinates: Quantitative RCC relations using coordinates of MBRs.
   Reasoning using Pellet.
c) RCC5 and RCC8: Combined qualitative and quantitative representation.
   Reasoning using Pellet
