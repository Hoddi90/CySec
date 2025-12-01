---
tags:
  - Category/Lecture-Notes
aliases:
  - Lecture-Note
---


# Phishing Detection, ML Evasion & Visual-Based Defenses

**Date:** {{date}}
**Created:** {{time}}

---

## Key Concepts & Takeaways

- Phishing continues to grow; most defenses still rely on **blocklists**, which are reactive.
- ML-based phishing detection uses **URL**, **HTML/DOM**, **reputation**, and **visual similarity** features.
- Reference-based detectors (e.g., logo matching) work well only when the brand is known and the logo is not modified.
- Attackers can evade feature-based and visual-based systems using **simple manipulations** or **adversarial perturbations**.
- GAP and LogoMorph show that **small, human-imperceptible modifications** can fool ML detectors.
- Human users often do **not rely on logos** when judging page legitimacy.
- Explainable AI (e.g., LIME) provides visibility into model decisions but has **limited reliability** and can itself be attacked.

---

## Connections to Earlier Material

- **ML Evasion → Security Principles:** Relates to the idea that attackers adapt faster than defenders; no single mechanism is foolproof.
- **Visual Similarity Detection → Human Factors:** Even perfect detectors do not guarantee user safety if humans overlook visual cues.
- **Adversarial Perturbations → OS & App Security:** Similar to buffer overflow exploits—small, precise manipulations can create large security failures.
- **Blocklists → Threat Intelligence:** Same limitations as signature-based antivirus tools.

---

## Questions for Discussion / Research

- Why do simple HTML/URL manipulations still bypass state-of-the-art ML systems?
- Should phishing detectors prioritize visual similarity, behavioral signals, or user interaction patterns?
- What would a defense look like that is robust against both ML evasion and human fallibility?
- Could browser vendors enforce rendering constraints that reduce adversarial logo attacks?
- How transferable are adversarial perturbations between different ML architectures?

---

## Diagrams / Examples / Code

### Example: ML Phishing Detection Pipeline
- Shows how URL/HTML features feed into the classifier.

```python
# Simplified pipeline
features = extract_features(webpage)     # URL length, entropy, DOM ratios, logo features
prediction = model.predict(features)     # benign / phishing
return prediction
```

---

### Diagram: Reference-Based Logo Detector
- Demonstrates how a suspected logo is matched against known brand logos.

```text
[Extracted Logo] → [Feature Encoder] → [Logo Database]
                                   ↘ match? ↙
                             If similar & domain mismatch → phishing
```

---

### Example: Simple Evasion via HTML Injection
- Modifies feature distribution while appearing identical to users.

```html
<!-- Invisible noise to confuse DOM-based detectors -->
<div style="display:none">
    AAAAAAAA BBBBBBBB CCCCCCCC
</div>
```

---

### Example: Adversarial Logo Perturbation (GAP-like logic)
- Perturbs pixels to fool the classifier while preserving human appearance.

```python
# pseudo-GAP step
logo = load_image("target_logo.png")
perturb = epsilon * sign(gradient(model, logo))
adv_logo = logo + perturb
```

