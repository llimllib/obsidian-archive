https://ferd.ca/notes/paper-you-want-my-password-or-a-dead-patient.html via [this toot](https://elk.pwm.social/hachyderm.io/@neilmadden@infosec.exchange/111475577364772328) via [Greg Wilson](https://mastodon.social/@gvwilson)

is a summary of [this superby-titled paper](https://www.cs.dartmouth.edu/~sws/pubs/ksbk15-draft.pdf) by Koppel et al ([here it is on pubmed](https://pubmed.ncbi.nlm.nih.gov/25676976/)).

I have long thought that each department in a major hospital (and in many other large teams in businesses) should have a programmer embedded with the team to support them in making the computers useful to them rather than a hindrance, and this paper provides great support for that belief.

(Of course, the systems themselves should be constructed to allow these sorts of modifications by their users - but that's a larger problem than I'm going to get into here)

Some quotes from the paper:

> The humans who build, use, and maintain the systems... did not sufficiently consider the actual clinical workflow. For example, the bolus of passwords, each with specific requirements and time limits, are seen as an annoyance, not as a patient safety effort.

My wife is a physician, and I can attest that from her experience this is absolutely the case. Doctors in the ER spend a large amount of their time and effort circumventing restrictions that are well-intentioned but make their day to day work insufferably annoying.

> We find, in fact, that workarounds to cyber security are the norm, rather than the exception. They not only go unpunished, they go unnoticed in most settings—and often are taught as correct practice.

except when inspection time comes, and the hospital gets dinged for breaking the rules because, for example, doctors and nurses remove "privacy screens" from computer monitors that make it impossible to actually see the screen.

> in healthcare, we see endemic circumvention of password-based authentication. In hospital after hospital and clinic after clinic, we find users write down passwords everywhere. Sticky notes form sticky stalagmites on medical devices and in medication preparation rooms. We’ve observed entire hospital units share a password to a medical device, where the password is taped onto the device. We found emergency room supply rooms with locked doors where the lock code was written on the door--no one wanted to prevent a clinician from obtaining emergency supplies because they didn’t remember the code.

> She saw clinicians offering their logged-in session to the next clinician as a “professional courtesy,” even during security training sessions.

Passwords simply do not work in these scenarios and IT often tries to just Password Harder to Increase Security

> one hospital’s EMR prevented users from logging in if they were already logged in somewhere else, although it would not meaningfully identify where the offending session was... when a nurse going into surgery discovered she was still logged-in, she’d either have to un-gown—or yell for a colleague in the non-sterile area to interrupt her work and go log her out.

> At one hospital, nurses in pre-op need to physically move patients to the OR, which is 2 minutes away. It's important to the OR people that the time of the transfer into the OR is accurately recorded (to the minute). But the patient record (and the EMR portal) is at pre-op, not in the doorway to the OR. When the hospital had a paper-based EMR, the nurses would enter “current time + 2 min” into the paper record before rolling the patient down the hall. However, the new EMR does not allow future times; consequently, the nurses leave themselves logged in but turn the monitor off – and then come back to the pre-op afterward and record the OR transfer time.

These sorts of solutions to artificial problems are absolutely normal in the hospital, waste time, and reduce patient welfare.

