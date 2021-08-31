IETF - ROLL Interim Meeting
15:00 to 16:30 UTC - Tuesday 31th August 2021
Material
https://datatracker.ietf.org/meeting/interim-2021-roll-02/session/roll
https://github.com/roll-wg/ROLL-Interim-Meeting

Meetecho: https://meetings.conf.meetecho.com/interim/?short=e89314d3-d762-4877-8f84-1108420ad8a4

Agenda
Time (UTC)	Duration	Draft/Topic	Presenter
15:00 - 15:05	5 min	WG Status	Ines/Dominique
15:05 - 15:35	30 min	draft-ietf-roll-enrollment-priority	Michael/Pascal
15:35 - 16:05	30 min	draft-iwanicki-roll-rnfd	Konrad
16:05 - 16:25	20 min	draft-ietf-roll-dao-projection	Pascal
16:25 - 16:30	5 min	Open Floor	Everyone
Meeting notes
[15:00] Meeting starts
note well
[15:02] WG Status
storing-rootack: chairs will raise question again on the ML

bier-ccast? Pascal: other priorities at the time. Carsten (re ietf-roll-ccast): had an implementation effort, no longer active. So status is waiting for implementation resources.

nsa sitting in Alvaro’s queue

[15:11] draft-ietf-roll-enrollment-priority (Michael and Pascal)
thought was done, then new issues raised.

recently merged in the total DODAG size info (used to be a separate draft)

issue: is min_priority change a change for Trickle?

Pascal: first decide if nodes can change the min_priority as it goes down the DODAG. Now think should not change across teh DODAG. Does not affect 9032.

Rahul: not change min_priority will simplify things, but intermediate should be able to say “don’t join” if out of resources.

Pascal: which resources?

Rahul: Neighbor table, for example

Pascal: this priority affects nodes not already part of the DAODAG.

MCR: local node can take this min-priority and add local value

MCR: no capacity for new node to join, node could increment the min_priority

Pascal: first question: is min_priority incremented going the DODAG. We agree the answer is “incremented only locally”, not propagated

Konrad: only use case is disabling joining in a sub DODAG.

Pascal: this value does not control the shape of the DODAG. Should not interact with routing.

Pascal: sequencing argument is valid

MCR: need an additional counter. If we have, can we increment down the DODAG

Pascal: incremening down the DODAG is not what we want

Pascal: think use case where node moves from one DODAG to another one, multiple PANS. You want to balance them. Decide which DODAG you want to join.

Rahul: wanted to shut off new nodes joining this router, to balance the tree.

Pascal: this use-case requires more than this priority.

MCR: still dont know how to turn joining on and off, globally. Needs another lollipo counter. Interacts with Trickle if in DIO. Another distribution mechanism?

Pascal: if constant, perfectly fine with Trickle.

Konrad: if GLOBAL approach; also consistent with DODAG size.

MCR: add lollipo counter. Will update the doc

Rahul:

Pascal: still need to define how the leaf augments the min_priority locally. Will discuss on ML.

[15:42] draft-iwanicki-roll-rnfd (Konrad)
describes use case

in pratice, what exactly happens depends on implementation

Increase control traffic due to root crash

RNFD aims to minimize time and traffic, need additional option

Design principle, goal to make it independent of RPL, so does not affect Protocol enormously

Coordination of nodes to detect failure

No wait to have a lot of traffic to detect crash =>

Proactive checking

Pascal: Sentinels are one hop away from root ? they can talk together through the LBR, if it is up

Description of the proposed solution: Sentinels, Acceptors, LORS, CFRC, RNFD Option, State machine,

Pascal: “sufficeient” sentinel. How do they communicate if the root id down?

Konrad: they don’t. Merging of CFRC . If netwrok is sparse, (cross shape) …

Pascal: parameters have good threshold values that depend on topology. Suggest to consider to communicate through the root, and multicast to sentinels.

Pascal: all first hops should declare that root is down, pretty much at the same time. Failure to receive this message in Trickle period would case them to ping the Root aggressively and declare it dead quickly. Will float the DODAGs.

Pascal: recommend to think about the propoerties you want your protocol to acheive.

Dominique: adoption? may need a charter adjustment.

mcr: maintenance of RPL should be in our charter (from meetecho chat)

Pascal: standards track or experimental? suggesting experimental. Think backward compatibility.

Dominique: Confirm in ML

[16:15] draft-ietf-roll-dao-projection (Pascal)
thanks to Toerless for extensive review

-20 in progress

added the concept of Leg.

Losse sequence of nodes between ingress and egress

Policies to inject traffic out of scope

Do not do detnet in the draft

from Anand’s review, clarify how to improve reliability of P-DAO injection

could build real DODAG instead of just parallel legs.

More complexity at ingress node, but more benefits. Exactly what RAW wants.

could go into another draft.

Pascal suggests to throw this into this draft before shipping.

[16:40] Meeting adjourned
