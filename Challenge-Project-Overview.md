# AI Companion Risk Radar: Classifying User-Reported Risk Themes in Mental Health App Reviews

**Company / Org:** Cornell Brooks School of Public Policy
**Challenge Advisor:** Ibrahim Emara, [ie68@cornell.edu](mailto:ie68@cornell.edu)
**AI Studio Coach:** Shaun Figueiro, [shaun.figueiro@breakthroughtech.org](mailto:shaun.figueiro@breakthroughtech.org)
**Program:** Break Through Tech AI Studio - Fall 2026

---

## 🏢 About Cornell Brooks School of Public Policy

The Jeb E. Brooks School of Public Policy at Cornell University advances the well-being of people through policy research, training, and engagement. The School prepares students to use evidence and analysis to address pressing public-policy challenges in the United States and globally.

---

## 🎯 The Challenge

### Project Summary

In this project, you will use public mental health app review data and natural language processing (NLP) and supervised classification techniques to build a model that classifies user-reported risk themes in app reviews, such as dependence, attachment, isolation, crisis-response frustration, or other concerns.

This project aims to help product, trust and safety, compliance, and app-quality teams identify recurring user-risk signals that may not be visible from star ratings or safety policies alone.

The project focuses on identifying patterns in public user reviews. It is not intended to diagnose users, evaluate clinical effectiveness, or establish that an AI tool caused a particular mental-health outcome.

### Success Criteria

A successful December outcome would include:

* A cleaned and documented review dataset or subset.
* A clear risk-theme annotation codebook.
* A hand-labeled training sample with documented labeling decisions.
* At least one interpretable baseline classifier that predicts review-level risk themes.
* Model evaluation using macro F1, per-class precision/recall, and confusion matrices.
* Error analysis explaining where the model performs well or poorly.
* Plain-language interpretation of results for non-technical stakeholders.
* A final presentation summarizing the methodology, findings, limitations, and potential applications.

### Stretch Goals

If the team progresses quickly, the main stretch goal is a **Temporal Risk Theme Dashboard**.

The team could aggregate classified reviews by app, risk theme, and week or month to explore whether specific themes increase over time or cluster around particular tools. A further extension could compare AI/chatbot-relevant apps with the broader set of mental health apps in the dataset.

### Project Milestones

Use these milestones to guide your work. Your team will create a **GitHub Projects board** to break each milestone into manageable tasks.

| Month         | Milestone                                          | Key Activities                                                                                                                                                                                                                                                                    |
| ------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **August**    | Kickoff and project setup                          | Review the project scope and datasets; confirm team roles; set up the working environment; review the proposed risk-theme categories; begin identifying AI/chatbot-relevant apps within MHARD.                                                                                    |
| **September** | Data exploration, preprocessing, and label design  | Explore review text, app names, ratings, dates, likes, and other metadata; document missing values and duplicates; define inclusion/exclusion criteria for AI/chatbot-relevant apps; finalize the risk-theme codebook; hand-label a training sample and review label consistency. |
| **October**   | Baseline modeling and model comparison             | Convert review text into model-ready features using TF-IDF; train an interpretable baseline such as logistic regression; compare with at least one additional classification approach; examine class imbalance and model errors.                                                  |
| **November**  | Evaluation, interpretation, and optional dashboard | Evaluate models using macro F1, per-class precision/recall, and confusion matrices; conduct error analysis; identify interpretable features or patterns associated with each class; if time allows, begin the temporal dashboard.                                                 |
| **December**  | Final deliverables and presentation                | Finalize the model and documentation; summarize findings and limitations in plain language; polish any dashboard or visualizations; prepare and deliver the final AI Studio presentation.                                                                                         |

> **Note for the team:** Please create a GitHub Projects board in this repository to break these milestones into weekly tasks. Go to **Projects → New project → Board**.

---

## 📊 Dataset

### Primary Dataset: MHARD — Mental Health App Reviews Dataset

**Name and Source:** MHARD — Mental Health App Reviews Dataset, Sensify Lab
**Format:** CSV (`MHARD_dataset.csv`)
**Size:** Approximately 75.7 MB
**Location:** https://github.com/Sensify-Lab/MHARD

### Key Details

* Contains approximately 200,000 Google Play reviews from 73 mental health apps.
* Relevant fields include:

  * `UID` — unique review identifier
  * `app_name` — app name
  * `rating` — user rating from 1–5
  * `date` — review date
  * `review` — original review text
  * `review_cleaned` — preprocessed review text
  * `likes` — number of likes
  * `response` — developer response, when available
* The dataset includes both AI/chatbot-related and broader mental health apps. The team should document clear criteria for selecting the subset most relevant to this project.
* The dataset does **not** contain the risk-theme labels needed for this project. The team will create a hand-labeled training sample using the annotation guidelines below.
* Some fields contain missing values, including developer responses and some existing model-generated predictions.

### Supplementary Reference Dataset: AI-Mediated Mental Health Support on Reddit

**Name and Source:** *AI-Mediated Mental Health Support on Reddit: Annotated Dataset of 5,126 Posts Across 47 Communities* — Aghakhani & Rezapour (2026), Zenodo
**Format:** CSV
**Size:** Approximately 2.3 MB
**Location:** https://zenodo.org/records/18751157

This dataset contains 5,126 posts from 47 mental health-related subreddits discussing AI use for emotional support and therapy-related purposes. It includes annotations for perceived usefulness, trust, risk, bond, sentiment, usage intent, and comparison to human therapy.

Because raw Reddit post text is not included, this dataset should primarily serve as a **reference for understanding AI-mediated mental-health use and informing the risk-theme taxonomy**, rather than as the main dataset for text classification.

---

## 🛠️ Suggested Approach

**Core ML Problem Types:** Classification and Natural Language Processing (NLP)
**Stretch Goal:** Time-series aggregation and dashboarding

### Recommended Libraries

* `pandas` — data loading, cleaning, and exploration
* `numpy` — basic numerical operations
* `scikit-learn` — TF-IDF, classification models, train/test splitting, and evaluation
* `matplotlib` — exploratory and model-performance visualizations
* `plotly` or `streamlit` — optional dashboard development

### Step 1: Data Cleaning and Exploration

Before modeling:

1. Inspect missing values and duplicate reviews.
2. Review the distribution of apps, ratings, dates, and review lengths.
3. Define and document which apps will be treated as AI/chatbot-relevant.
4. Retain fields needed for analysis, including review text, app name, rating, date, and likes.
5. Document every major cleaning or filtering decision so the workflow is reproducible.

Avoid removing words or phrases that may carry meaning relevant to dependence, attachment, isolation, or frustration.

### Step 2: Risk-Theme Annotation

Use the following categories as a **starting codebook**. The team may refine the definitions with the Challenge Advisor before full labeling begins.

* **Dependence:** The review suggests reliance on the tool, difficulty reducing use, or a perceived need to continue using it for emotional support.
* **Attachment:** The review describes an emotional bond, relationship, affection, or sense of connection with the tool.
* **Isolation / Displacement:** The review suggests the tool is replacing, reducing, or being preferred over interaction with other people or sources of human support.
* **Crisis-Response Frustration:** The review criticizes, expresses dissatisfaction with, or describes problems with the tool's handling of crisis, safety, or referral situations.
* **Other / None:** The review does not clearly fit one of the target risk themes.

Before labeling the full training sample:

1. Label a small pilot sample.
2. Discuss ambiguous examples and refine the codebook.
3. Have at least two team members independently label a portion of the same reviews.
4. Compare disagreements and document how they are resolved.
5. If feasible, calculate an inter-rater agreement measure such as Cohen's kappa.

### Step 3: Baseline Modeling

Start with an interpretable baseline:

1. Convert review text into TF-IDF features.
2. Train a logistic regression classifier.
3. Compare the baseline with at least one additional model, such as random forest or another appropriate supervised classifier.
4. Address class imbalance if necessary.

More complex NLP models may be explored only after the baseline pipeline is working reliably.

### Step 4: Evaluation and Interpretation

**Primary evaluation metric:**

* Macro F1

**Additional metrics:**

* Per-class precision
* Per-class recall
* Confusion matrix

Because the final audience may include non-technical stakeholders, model performance should also be explained in plain language.

Where possible, interpret:

* Which words or features contribute most strongly to different classifications.
* Which risk themes are easiest or hardest to distinguish.
* Common patterns in misclassified reviews.
* Important limitations that stakeholders should understand before using the results.

---

## 📚 Resources to Get Started

### Background Reading

* **MHARD Dataset and Documentation:**
  https://github.com/Sensify-Lab/MHARD

* **Wang et al. (2025), "Leveraging Large Language Models for Review Classification and Rating Estimation of Mental Health Applications":**
  https://doi.org/10.1609/icwsm.v19i1.35916

* **Cooper et al. (2026), "Framing Responsible Design of AI Mental Well-Being Support: AI as Primary Care, Nutritional Supplement, or Yoga Instructor?":**
  https://doi.org/10.1145/3772318.3791556

### Technical Tutorials and Documentation

* **Scikit-learn: Working With Text Data:**
  https://scikit-learn.org/stable/tutorial/text_analytics/working_with_text_data.html

* **Scikit-learn: Model Evaluation and Classification Metrics:**
  https://scikit-learn.org/stable/modules/model_evaluation.html

* **Scikit-learn: Logistic Regression:**
  https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression

### Optional Dashboard Resource

* **Streamlit Documentation:**
  https://docs.streamlit.io/

*You are encouraged to explore beyond these resources and share useful findings with the team.*

---

## 🤝 How We'll Work Together

**Official check-ins:**
We will meet during the assigned **60-minute AI Studio Lab Section block on the second and fourth week of each month**.

**Communication outside official check-ins:**

* Use the team's channel in the Break Through Tech Discord workspace for routine project questions.
* Email the Challenge Advisor when a question requires direct follow-up; please copy the AI Studio Coach when relevant to the whole team.
* Technical debugging, detailed Python questions, GitHub troubleshooting, and day-to-day project management should generally be directed to the AI Studio Coach.
* Additional Zoom meetings may be scheduled when necessary and as availability allows.

**Response time:**
I will aim to respond within **48 hours on weekdays**. For urgent technical questions, please contact the AI Studio Coach.

### Recommended Free Tools

* **Coding / analysis:** Google Colab or Jupyter Notebook
* **Version control and project tracking:** GitHub and GitHub Projects
* **Communication:** Break Through Tech Discord
* **Virtual meetings:** Zoom

---

## 🚀 Getting Started

1. **Read this overview** and note any questions for our first meeting.
2. **Open the MHARD repository** and review its README, dataset fields, and sample data.
3. **Review the supplementary Reddit dataset** to understand how previous researchers have categorized AI-mediated mental-health experiences.
4. **Read the GitHub Projects documentation** here:
   https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects
5. Come to our first meeting prepared to discuss:

   * Initial questions about the project
   * Which apps may belong in the AI/chatbot-relevant subset
   * Any risk-theme definitions that seem unclear

Looking forward to working with you all!

---

## ❓ Questions?

Please bring any questions to our first meeting during the week of August 24th (Break Through Tech’s Bridge to Studio - Session C).
