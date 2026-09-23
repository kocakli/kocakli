# Day 4 draft notes

## Word counts

Body counts exclude YAML frontmatter and use a Unicode word-token count.

- EN: 1,268 words
- TR: 1,047 words

## Outbound URLs used

- https://github.com/cobanov/awesome-jev
- https://github.com/leepokai/jev-guard
- https://github.com/qkal/Canny
- https://github.com/shitianfang/wakegate
- https://github.com/luantak/is-malicious
- https://openrouter.ai/docs/cookbook/building-agents/gate-tool-calls-with-jev
- https://typesafe.ai/blog/introducing-system-one-models-and-jev

## Internal URLs used

- https://www.oguzhan.co/typesafe-jev-system-one-decision-model/
- https://www.oguzhan.co/tr/typesafe-jev-system-one-karar-modeli/
- https://www.oguzhan.co/jev-speed-cost-parallel-sampler/
- https://www.oguzhan.co/tr/jev-hiz-maliyet-paralel-ornekleyici/

## FACTS gaps not filled

- FACTS provides no production-security certification for jev-guard, Canny, wakegate, or is-malicious. No certification claim was made.
- FACTS provides no attack-prevention rate or evidence that Jev stops every prompt injection. No such effectiveness claim was made.
- FACTS does not establish that a clean is-malicious result proves safety. The drafts state the opposite and do not extend the tool into antivirus, dependency CVE auditing, or secret scanning.
- The supplied latency figures belong to different project runs and locations. They were kept separate rather than presented as a direct benchmark comparison.
- FACTS does not say wakegate chooses a sleep interval. The drafts explicitly leave that function out.
