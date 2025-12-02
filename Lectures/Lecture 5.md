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
- Phishing Website Detection (via ML)
	- The detection of a phishing webpage can entail the analysis of various elements, e.g.:
		 • The URL of the webpage (e.g., long URLs are more likely suspicious)  
			• The HTML (e.g., phishing webpages have many elements hosted under a different domain)  
			• The ‘reputation’ of a webpage (e.g., a webpage whose domain has been active for a long time, or that is indexed in Google, is likely benign)  
			• The visual representation (through reference-based detectors)
 * Do feature-based detectors work?
	 * It is possible to develop good ML-based detectors by analysing various types of “features” (URL-based, HTML-based, or a combination thereof) and by using diverse types of ML algorithms, such as random forests (RF), logistic regression (LR), or convolutional neural networks (CN)
		 * Limitiation: extremly high consumption of resources
* ML methods are typically considered as black boxes
	* They are so complex, that it is hard for a human to explain what led the ML model to  
		produce any given output
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
- Which features are used by ML based phising website detectors?
	-  HTML structure(elements hosted under different domains)
	- The reputation of the webpage(e.g. Google indexing age)
	- The length and structure of the URL.
* What is a major limitiation of refrence-based(visual simularity) detectors?
	* They only work on websites included in their "protected" refrence list 
*  Under what condition is an adversiarial atttack against a logo detector most effective?
	* When the attacker and defender use the exact sam Deep Learning model.
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

