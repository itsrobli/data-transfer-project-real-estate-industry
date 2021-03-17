# Background and goals

In the real estate industry, we exchange a lot of data with each other (due to all the JVs). I sadly watch a bunch of finance people translating each other’s spreadsheets into the correct format (schema) for their home systems using the worst tools that exist (VLOOKUP + Copy and Paste + typing). This is every month of their lives.

Maybe we can tackle this from an engineering level up? Can we define an interchange format and process? And share the tools (scripts) to do these tasks?

Let's run this like an open source project and see what happens.

# Proposal

1.	Define a common schema / or data exchange format that will evolve over time. Something like this used in other industries 
  - https://github.com/google/data-transfer-project - an initiative setup between the big tech companies to incrase data portability (\*cough\* GDPR)
  - https://www.hl7.org/implement/standards/.

2.	Share scripts that convert from our system’s schema to that common schema and back.

3.	We can start with basic use cases like moving our Cougar/MRI data around. Or sharing sales metrics.

No real data should to exist in this repo other than for testing (which can be masked).

## Example

**Base case**

Mirvac -> Generic -> AMPCRE  

This is the work AMPCRE would do. Because someone has to start so AMPRCRE would have to do it anyway.

**Let’s say Charter Hall is also JV’d with Mirvac.**

Charter Hall would need to go:

Mirvac -> Generic -> Charter Hall

Charter Hall only has to do half the work because the first leg would be donated to this repo. So Charter Hall would be incentivised to sign-up to leverage the Mirvac -> Generic leg of the interchange.

Now Charter Hall has created and contributed Generic -> Charter Hall.

**So let’s say Charter Hall has a JV with a randomREIT.**

Charter Hall would contribute

randomREIT -> Generic -> Charter Hall

Now if AMPCRE has a JV with randomREIT as well – it would be already done. 

Take Charter Hall’s randomREIT -> Generic. Mary it up with Generic -> AMPCRE.

