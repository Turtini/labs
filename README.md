## How to use these labs

These labs are designed to be **studied and practiced**, not executed as automation.

Each lab represents a *type of task* commonly encountered by Linux system
administrators and evaluated in hands-on certification environments such as RHCSA.

### Recommended approach

1. **Read the lab README first**
   - Understand the objective and the initial system state.
   - Pay attention to what is explicitly required — and what is not.

2. **Think before typing**
   - Ask yourself: *Which Linux primitives solve this problem?*
   - Avoid shortcuts or aliases you wouldn’t rely on under pressure.

3. **Type the commands manually**
   - Use the `commands.md` file as a reference, not a script.
   - Build muscle memory for correct syntax and sequencing.

4. **Verify the result**
   - Always confirm your work using inspection commands (`getent`, `id`, `ls -l`, `systemctl`, etc.).
   - Do not assume success based on lack of errors.

5. **Repeat without notes**
   - Re-run the lab from memory.
   - Speed and confidence come from repetition, not explanation alone.

### What these labs are (and are not)

- ✅ These labs teach **skills, patterns, and verification habits**
- ✅ They align with publicly documented Linux administration objectives
- ❌ They do not reproduce exam questions
- ❌ They do not automate solutions
- ❌ They are not a substitute for hands-on practice

### Environment expectations

- A RHEL-compatible system (RHEL, Rocky, Alma, CentOS Stream)
- Root or sudo access
- SELinux enforcing (do not disable unless explicitly instructed)
- No internet access required during practice

### Philosophy

The goal of these labs is not to “get through a task,” but to develop
**calm, repeatable system administration under constraint**.

If you can complete these labs cleanly, verify your work, and explain
*why* each command exists, you are building the exact instincts
required for real-world operations — and for hands-on exams.
