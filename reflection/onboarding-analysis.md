# Onboarding analysis

The user journey from install → first useful task → sustained use. I went through this myself. This is my experience, analyzed as a product person.

---

## Phase 1: Install

**What happened:** I installed Hermes via the shell installer (`curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash`). It bootstrapped the Python environment, dependencies, and the launcher. The install was clean — no manual dependency resolution, no broken paths.

**What worked:** The installer handled everything. I didn't need to know Python or virtual environments — it just worked.

**What nearly stopped me:** Nothing, at this stage. The installer is the strongest part of the journey — it's a single command and it sets up the whole environment.

**Friction point:** The installer sets up the CLI. I didn't realize there was also a desktop app until later. The discovery path from "I installed the CLI" to "there's a desktop app with a GUI" wasn't obvious.

## Phase 2: First run — setup and model selection

**What happened:** I ran `hermes setup` — a setup wizard that walked me through picking a model and provider. I chose my default inference endpoint. The setup wizard configured `config.yaml` and I was ready to go.

**What worked:** The setup wizard is well-designed — it doesn't overwhelm with options. It asks what you need and configures the rest.

**What nearly stopped me:** I didn't know what model to pick. The setup wizard offered choices, but I didn't have a frame of reference for which model was good for what. I picked the default because it was the default, not because I evaluated models. A new user without context might stall here.

**Friction point:** The model selection step needs a "what is this for" frame, not just a list of model names. "GLM-5.2 is good for general tasks, fast, and cost-effective" is more helpful than "GLM-5.2."

## Phase 3: First useful task

**What happened:** My first useful task was asking Hermes to read my resume PDF and help me organize my project repos. It read the PDF, pulled my GitHub profile, listed my repos, and proposed a structure for organizing them. That was the first moment I thought "oh, this is actually useful."

**What worked:** The agent read a file, accessed the web, and produced a useful output in one conversation. I didn't have to switch tools or copy-paste between contexts. The file-reading capability was the hook — it meant Hermes could see what I was working on, not just what I typed.

**What nearly stopped me:** I had to learn what Hermes *could* do. The first task was useful, but I didn't know the range of capabilities until I'd used it for a while. The discovery of skills, memory, cron, and the Telegram gateway happened over days, not in the first session.

**Friction point:** The first-session experience doesn't surface the range of capabilities. I discovered skills by seeing the "available skills" list in the system prompt; I discovered memory by noticing Hermes remembered things across sessions; I discovered the Telegram gateway by reading the docs. A guided "here's what you can do" flow after setup would accelerate activation.

## Phase 4: Sustained use — the trust ramp

**What happened:** Over the first week, I started trusting Hermes with more. First simple tasks (read this file, search for this). Then medium tasks (build a skill, write a section of a document). Then complex tasks (run a pre-publish review with secrets scanning, clean-install verification, and test execution). Then I connected the Telegram gateway so I could work from my phone.

**The moment I started trusting it with more:** The pre-publish review. Hermes scanned for secrets, ran a clean install, executed tests, and produced a detailed verification report — all through a conversation. That was the moment I thought "I trust this with my real work." It wasn't the first task; it was maybe the fiftieth.

**What made the difference:** 
1. **Memory.** Hermes remembered my projects, my preferences, my working style. I didn't re-explain.
2. **Skills.** I built my own skills — the agent learned how I work and loaded that knowledge when relevant.
3. **Honest failure.** When things broke (stale write protection, compression losses), Hermes said so. The honesty built trust faster than a fake success would have.
4. **Visible value.** I could see what Hermes did — the files it wrote, the commands it ran, the outputs it produced. The value was legible and traceable.

**Friction point:** The trust ramp took about a week. That's a long time for a product to prove itself. The risk is that users drop off before the trust ramp kicks in — they use it for simple tasks, don't experience the depth, and leave. The product needs to accelerate the trust ramp: surface the "Hermes can do your real work" moment earlier.

## Phase 5: Where I am now

I use Hermes daily. I've built 3 custom skills. I have 20+ uses of the hermes-agent skill. I have persistent memory that remembers who I am and how I work. I have a Telegram gateway that lets me work from my phone. I've shipped 4 public projects with Hermes as collaborator. This repo itself was built entirely through Hermes sessions.

The journey from install to here took about 3 weeks. The product earned my trust through the four pillars: memory, skills, honest failure, visible value. The product opportunity is shortening that journey — getting more users to the trust ramp faster.

---

## What this shows

The "own the user journey from installation and setup to a first useful task and sustained use" requirement, told as my actual experience. Not a funnel analysis — a lived account of going through the journey myself and noticing where it works, where it drops off, and what I'd change.

The key insight: activation (first useful task) is necessary but not sufficient. The product lives or dies at the trust ramp — the journey from "I use it for simple tasks" to "I trust it with my real work." That's where Hermes succeeds (it got me there) and where the opportunity is (it took a week; it should take less).
