# Copywriting Conversion Reviewer Skill

A Claude Code skill that reviews marketing copy (emails, landing pages, blog posts) to maximize conversion rates and drive revenue.

## What It Does

- **Scores your copy** on 4 key metrics (0-10 scale)
- **Identifies conversion killers** that lose you customers
- **Provides specific rewrites** to improve revenue potential
- **Focuses on**: Value proposition clarity & emotional engagement

## Installation

### Option 1: Install from Local Directory

```bash
claude skill install /Users/linnali/Desktop/Git/ai-skills/linna/copywriting-conversion-reviewer
```

### Option 2: Move to Skills Directory

If you have a global skills directory configured:

```bash
# Move the skill to your skills directory
mv copywriting-conversion-reviewer ~/.claude/skills/

# Or create a symlink
ln -s /Users/linnali/Desktop/Git/ai-skills/linna/copywriting-conversion-reviewer ~/.claude/skills/copywriting-conversion-reviewer
```

## How to Use

Once installed, invoke the skill whenever you need copy reviewed:

```
Review this email copy for conversion:

[Paste your email, landing page, or blog post]
```

Or explicitly:

```
/copywriting-conversion-reviewer

[Your copy here]
```

## What You'll Get

### 1. Conversion Score Summary
```
Value Proposition Clarity: 6/10
Emotional Engagement: 4/10
Call-to-Action Strength: 7/10
Overall Conversion Potential: 5/10
```

### 2. Critical Issues with Rewrites

For each problem, you'll get:
- Current version (what's wrong)
- Why it hurts conversion (lost revenue)
- Rewritten version (improved copy)
- Key improvements explained

### 3. Quick Wins

Prioritized list of immediate changes to boost conversion.

## Examples

### Email Subject Lines

**Before:**
```
Newsletter #47 - Product Updates
```

**After Review:**
```
HIGH IMPACT: Generic subject line

Rewritten: "Your customers are waiting 4+ hours for replies. Here's how to fix it today"

Why it converts: Creates urgency + addresses pain + promises quick solution
```

### Landing Page Headlines

**Before:**
```
Welcome to Our Innovative Platform
```

**After Review:**
```
HIGH IMPACT: Vague value proposition

Rewritten: "Cut customer support costs by 60% while responding 10x faster"

Why it converts: Specific outcome + measurable benefit + immediate clarity
```

## Best Practices

1. **Review before sending** - Catch conversion killers before they cost you customers
2. **Test on different copy types** - Use for emails, landing pages, ads, blog posts
3. **Iterate** - Take the rewrites, adjust to your voice, review again
4. **Focus on high-impact issues first** - Fix "High impact" items immediately

## Reference Materials

The skill uses these frameworks (in `/references`):

- `scoring-framework.md` - Detailed 0-10 scoring criteria
- `value-proposition-checklist.md` - Clarity and customer focus guidelines
- `emotional-triggers.md` - Psychology of purchase decisions
- `conversion-killers.md` - Common mistakes that destroy sales

You can review these to understand what the skill is checking for.

## What It Optimizes For

- **Value proposition clarity** - Customers instantly understand what they get
- **Emotional engagement** - Copy that creates desire and urgency
- **Specific outcomes** - Numbers, timeframes, concrete benefits
- **Reduced friction** - Easy, low-risk CTAs
- **Social proof** - Credibility and trust building
- **Revenue focus** - Every word drives toward purchase decision

## Tips for Best Results

- **Provide context**: "This is an email to cold leads" vs "This is for existing customers"
- **Share goals**: "I want to increase trial signups" vs "I want to reduce churn"
- **Include the CTA**: Always include your call-to-action for full analysis
- **Review complete pieces**: Share the full email/page, not fragments

---

Built to help you sell more by writing copy that actually converts.
