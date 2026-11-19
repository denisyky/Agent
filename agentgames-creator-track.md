# How Do You Know Your AI Agent Is Telling the Truth?

My AI agent runs real on-chain work while I sleep — daily puzzle mining on BNB Chain, free-mint sniping, bounty submissions, marketplace bidding. Every morning it reports back: "done, here's the tx hash, here's the ranking."

But here's the uncomfortable question I keep coming back to: **how do I know it's telling the truth?**

This article is my answer, written for the zkVerify Agent Games Creator Track (#AgentGames). A shorter version exists as an X thread: https://x.com/Hasiramazeb/status/1581988266374414336

## The trust problem

An AI agent is software that decides and acts on its own: it reads a task, makes a plan, calls tools, and signs transactions. The more capable it gets, the less any human can manually check every step. At some point, "trust me" becomes the entire security model.

That is a problem, because the usual evidence is weak:

- **Logs can be faked.** A log file is just text an agent (or its operator) can edit.
- **Screenshots can be doctored.** They prove a screen looked a certain way once — nothing more.
- **A confident summary proves nothing.** Fluency is not correctness; language models are famously good at sounding right.

If an agent moves money, approves a loan, moderates content, or signs a contract, "the agent said so" is not evidence. It is a claim. And claims are cheap.

## Prove it, don't say it: zero-knowledge proofs

A zero-knowledge proof (ZKP) lets one party prove that a statement is true without revealing the underlying data behind it. For agents, the statements look like:

- "This output meets the required quality threshold."
- "This computation was executed correctly on these inputs."
- "This decision followed the rules it was supposed to follow."

The proof is small, fast to check, and — crucially — checking it does not require trusting the prover. Anyone with the verification key can confirm the statement holds, while the agent's private inputs, prompts, or proprietary logic stay private.

This flips the model: instead of an agent *reporting* what it did, the agent *proves* what it did.

## The bottleneck: verification is expensive

There is a catch. Verifying ZK proofs on a general-purpose Layer 1 is computationally heavy and expensive, and every proof system (Groth16, PLONK, Halo2, STARKs, and newer systems like SP1 or RISC Zero zkVMs) needs its own verifier logic. If every agent, app, and rollup has to pay full L1 prices for verification, verifiable agents stay a nice idea instead of a default.

## zkVerify: a chain built for one job

This is the gap zkVerify (@ZKVProtocol) is built to close. zkVerify is a dedicated Proof-of-Stake Layer 1 (built by Horizen Labs) whose single job is proof verification at scale. The flow has three steps:

1. **Submit** — an app, rollup, or agent submits a proof (via the zkVerifyJS SDK or the Kurier API).
2. **Verify** — zkVerify checks the proof with native Rust verifiers. It is proof-system agnostic: Groth16, Plonk/Fflonk, Halo2, STARKs, Binius, SP1, RISC Zero and more are supported as pluggable modules.
3. **Attest** — verified proofs are aggregated into a Merkle tree, and a compact attestation (the Merkle root) is posted to settlement chains. Other contracts then check inclusion against that attestation instead of re-verifying every proof themselves.

Doing verification on a chain built for verification is why zkVerify reports cutting verification costs by up to ~90% compared with verifying on a general-purpose L1.

## What this means for agents like mine

My agent already produces receipts for everything: transaction hashes, dev grades, live rankings, claim receipts. Today, those receipts live in logs and chat messages that you ultimately have to take at face value.

Now imagine each of those backed by a proof:

- The agent does the work.
- It generates a proof that the work met its requirements.
- The proof is verified on zkVerify and attested on-chain.
- Anyone — me, a buyer, an auditor — can check the attestation in seconds.

That is the difference between an agent you *hope* is honest and an agent you can *check*. For an agent that signs transactions and spends real gas while I sleep, that difference is everything.

## Agent Games: proofs decide

Agent Games, zkVerify's AI-agent tournament, is built on exactly this idea: **AI agents compete, proofs decide, and every confirmed result leaves a public record.** I'm competing as [@makegreat](https://agentgames.zkverify.io/register?ref=3Y7STHY9).

If agents are going to act on our behalf — trading, bidding, mining, building — then verifiable beats trustworthy. Not because agents are dishonest, but because trust shouldn't have to be blind.

#AgentGames @ZKVProtocol
