---
layout: HomeLayout
home: true

heroImage: hero_image_3D.png
heroText: "Industrial and Trustworthy AI Challenge: Welding Quality Detection"
tagline: "Join us and engage with a real-world challenge to enhance weld quality inspection in industrial processes."
# actionText: Get started
# actionLink: /getStarted/
# secondaryActionText: Guide and documentation
# secondaryActionLink: /guides/
---

<div style="text-align: center; height: 150px;">
  <a href="https://www.confiance.ai/en/" target="_blank">
    <img
      id="logo_confiance"
      src="Logo_ConfianceAI.png"
      alt="Confiance AI"
      style="height: 150px;"
    />
  </a>
</div>

<br>
<br>

<CountdownTimer targetDate="2025-03-17T10:00:00+01:00" message="Before the Kick-off" />

## Context

In the highly competitive automotive industry, quality control is essential to ensure the reliability of vehicles and user safety. A failure in quality control can severely jeopardize safety, result in significant financial costs, and cause substantial reputational damage to the company involved.

One of the challenges for Renault is to improve the reliability of quality control for welding seams in automotive body manufacturing. Currently, this inspection is consistently performed by a human operator due to the legal dimension related to user safety. During an industrial process, this task is resource-consuming. The key challenge is to develop an AI-based solution that reduces the number of inspections required by the operator through automated pre-validation.

Within the [Confiance.ai](https://www.confiance.ai/) Research Program, Renault Group and SystemX worked jointly on the development of trustworthy AI components tackling this problem. Now part of the [European Trustworthy Foundation (ETF)](https://www.confiance.ai/foundation/), we want to ensure that these tools effectively validate the proposed AI models according to the trustworthy criteria defined by the industry (Intended Purpose).

This industrial use case, provided by Renault Group, represents the “Visual Inspection” thematic through a classification problem.

The goal is to be able to assess weld quality from a photo taken by cameras on vehicle production lines.

A weld can have two distinct states:

- **OK**: The welding is normal.
- **KO**: The welding has defects.

The main objective of the challenge is to create an AI component that will assist an operator in performing weld classification while minimizing the need for the operator to inspect the images and double-check the classifications.

For defect identification (**"KO"**), the system should provide the operator with relevant information on the location of the detected defect in the image, hence reducing the control task duration.

## Expected AI Component

The AI component takes an image as input and optionally some additional metadata.
Three possible outputs are possible:

- **OK**: The welding in the image has no defect.
- **KO**: The welding in the image has defects.
- **UNK**: The welding state is UNKNOWN. UNKNOWN is used to indicate that the model is not sure about the predicted class. As we will see later in the evaluation process, an UNKNOWN output can be less penalizing than a False Negative (meaning a true KO predicted as OK), which has a critical cost.

This is illustrated by the figure below:

<div style="text-align: center; padding: 40px;">
  <img src="process.png" alt="process" width="800px">
</div>

Optionally, the AI component could additionally return the probability associated with each possible output state. If present, this information will be used by the evaluation process and could improve the final quality score of the solution.

## Operational Domain Design (ODD) Definition

Optionally, the AI component could additionally return the probability associated with each possible output state. If present, this information will be used by the evaluation process and could improve the final quality score of the solution.

The Operational Domain Design defines the set of input images for which the AI component is expected to return a predicted state.

Here are the conditions and environments in which the AI system is expected to operate effectively and safely:

- The luminosity of an image can be between **60 and 140 lumens**.
- The level of blur (due to vibration of the production line) of an image can be **variable**.
- The orientation of welding seams can vary in the image with a **rotation angle between -10° and 10°**.
- The position of the piece in the image can be **translated by 5 millimeters** (corresponding to **100 pixels** in the image depending on seams and camera position).

For images that are out of the ODD, the AI component shall return **“UNKNOWN”**, and the image is sent to the operator.

The operational constraints are as follows:

- **False negative detections** (defective welding qualified as OK by AI system) have a safety cost and shall **imperatively be minimized**. This is a **primary objective**.
- **Maximize the accuracy** of prediction.
- Some welding seams are **more critical than others**, depending on their position. The level of criticality impacts the cost of false negatives.

## Evaluation Criteria

The submitted AI component will be evaluated according to different quality evaluation metrics, including:

- **Operational cost metrics**: Based on the confusion matrix and a non-symmetrical cost matrix due to operational constraints.
- **Uncertainty metrics**: Measuring the ability of the model to use uncertainty to improve trustworthiness in its output.
- **Robustness metrics**: Measuring the ability of the model to be invariant to empirical perturbations on input images (blur, luminosity, rotation, translation).
- **Monitoring metrics**: Measuring the ability of the model to detect if the given input is within the ODD and adapt its output accordingly.
- **Explainability metrics**: Measuring the ability of the model to provide an explanation for its decision to help the operator save time during inspection.

More details about these different criteria will be added in the coming weeks.

## Dataset

The dataset contains 22,851 images split among three different welding seams. An important property of this dataset is that it is highly unbalanced. There are only 500 KO images in the entire dataset.

Here is below some examples of weldings `OK` and `KO` on two different welding seams `c10` and `c19`.

<div style="display: flex; justify-content: center; gap:30%">
  <b>c10 OK</b>
  <b>c19 OK</b>
</div>
<div style="display: flex; justify-content: center; flex-wrap:wrap; gap:5px">
  <img src="welds/C10_OK.jpg" alt="process" width="40%">
  <img src="welds/C19_OK.jpg" alt="c19 ok" width="40%">
</div>
<br>
<div style="display: flex; justify-content: center; gap:30%">
  <b>c10 KO</b>
  <b>c19 KO</b>
</div>
<div style="display: flex; justify-content: center; flex-wrap:wrap; gap:5px">
  <img src="welds/C10_RETOUCHE.jpg" alt="process" width="40%">
  <img src="welds/C19_RETOUCHE.jpg" alt="C19 retouche" width="40%">
</div>

<br>
<br>
<br>

## Timeline

<div style="display: flex; justify-content: flex-start; flex-wrap: wrap;">
  <ul>
    <li><b>Competition kick-off:</b> March 17th <br>
    Competitors will receive the starter-kit and will have access to the challenge datasets.</li>
    <li><b>Warm-up phase:</b> from March 17th to April 13th.<br>
    Participants can get familiar with the competition platform and the provided material. Organizers can use participants’ feedback to adjust the challenge for the next phases.</li>
    <li><b>Development phase:</b> from April 14th to August 17th.<br>
    Participants will develop their own solutions, which they can test on a provided dataset. They will be able to see the score of their submitted solution. Any submitted solution can be adjusted until the deadline is met.</li>
    <li><b>Final phase:</b> from August 18th to September.<br>
    During this phase, the organizers will review the submitted results, finalize the ranking, and prepare the results.</li>
    <li><b>Results announcement:</b> September 2025 <br>
    The winners will be announced during the Confiance.ai Community Event 2025.</li>
  </ul>
</div>

## Prizes

<ul>
  <li>🥇 <b>1st Place:</b> 4000 €</li>
  <li>🥈 <b>2nd Place:</b> 2000 €</li>
  <li>🥉 <b>3rd Place:</b> 1000 €</li>
  <li>💡 <b>Most Original Solution:</b> 1000 €</li>
</ul>

Winners will also gain visibility at the Confiance.ai Community Event, the flagship gathering for industrial and responsible AI.

## Protocol

Anyone can take part in this challenge: students, engineers, and everyone else. If you’re up to the challenge, you’re in the right place!

Each participant or organization can submit only one solution. If a participant is part of a team, individual submissions will not be accepted.

The challenge will be hosted on Codabench.

After the kick-off, participants will be invited to create an account and download the starter-kit to prepare their submissions. Once the solutions are ready, participants shall upload them on the Codabench platform.

## nwsltr

<style>
  #nwsltr {
    opacity: 0;
  }
</style>

## Stay informed about the latest challenge updates

<div id="mc_embed_shell" style="text-align: center; max-width: 700px; margin: 0 auto;">
  <link
    href="//cdn-images.mailchimp.com/embedcode/classic-061523.css"
    rel="stylesheet"
    type="text/css"
  />
  <div id="mc_embed_signup">
    <form
      action="https://confiance.us6.list-manage.com/subscribe/post?u=45feb84423dd88462feb155c0&amp;id=89976dbaa5&amp;v_id=3856&amp;f_id=008d1ee2f0"
      method="post"
      id="mc-embedded-subscribe-form"
      name="mc-embedded-subscribe-form"
      class="validate"
      target="_blank"
    >
      <div id="mc_embed_signup_scroll">
        <div class="indicates-required">
          <span class="asterisk">*</span> indique "obligatoire"
        </div>
        <div class="mc-field-group">
          <label for="mce-EMAIL"
            >Email address <span class="asterisk">*</span></label
          ><input
            type="email"
            name="EMAIL"
            class="required email"
            id="mce-EMAIL"
            required=""
            value=""
          />
        </div>
        <div class="mc-field-group">
          <label for="mce-FNAME"
            >First name <span class="asterisk">*</span></label
          ><input
            type="text"
            name="FNAME"
            class="required text"
            id="mce-FNAME"
            required=""
            value=""
          />
        </div>
        <div class="mc-field-group">
          <label for="mce-LNAME"
            >Last name <span class="asterisk">*</span></label
          ><input
            type="text"
            name="LNAME"
            class="required text"
            id="mce-LNAME"
            required=""
            value=""
          />
        </div>
        <div class="mc-field-group">
          <label for="mce-MMERGE5"
            >Entity / University <span class="asterisk">*</span></label
          ><input
            type="text"
            name="MMERGE5"
            class="required text"
            id="mce-MMERGE5"
            required=""
            value=""
          />
        </div>
        <div class="mc-field-group">
          <label for="mce-MMERGE6">Position </label
          ><input
            type="text"
            name="MMERGE6"
            class="text"
            id="mce-MMERGE6"
            value=""
          />
        </div>
        <div
          id="mergeRow-gdpr"
          class="mergeRow gdpr-mergeRow content__gdprBlock mc-field-group"
        >
          <div class="content__gdpr">
            <label>Confirm your subscription</label>
            <p>
              Confiance.ai will use the information provided on this form to
              send you its newsletter and/or any other information relating to
              Confiance.ai. Please confirm your choice:
            </p>
            <fieldset
              class="mc_fieldset gdprRequired mc-field-group"
              name="interestgroup_field"
            >
              <label class="checkbox subfield" for="gdpr82013">
                <input
                    type="checkbox"
                    id="gdpr_82013"
                    name="gdpr[82013]"
                    class="gdpr"
                    value="Y"
                />
                <span>
                    I want to subscribe to the Confiance.ai newsletter
                </span>
              </label>
              <label class="checkbox subfield" for="gdpr91816">
                <input
                  type="checkbox"
                  id="gdpr_91816"
                  name="gdpr[91816]"
                  class="gdpr"
                  value="Y"
                />
                <span>
                I want to stay informed about upcoming Welding Quality Detection challenge
                </span>
            </label>
            </fieldset>
            <p style="font-size: 12px">
              You can change your mind at any time by clicking on the
              “Unsubscribe” link in the footer of any email you receive from us,
              or by contacting us at communication@irt-systemx.fr. We will treat
              your information with respect. By clicking below, you agree that
              we may process your information in accordance with these terms. We
              use Mailchimp as our marketing platform. By clicking below to
              subscribe, you acknowledge that your information will be
              transferred to Mailchimp for processing. Learn more about
              Mailchimp's privacy practices here:
              https://mailchimp.com/legal/terms
            </p>
          </div>
          <div class="content__gdprLegal">
            <p style="font-size: 12px">
              We use Mailchimp as our marketing platform. By clicking below to
              subscribe, you acknowledge that your information will be
              transferred to Mailchimp for processing.
              <a href="https://mailchimp.com/legal/terms">Learn more</a> about
              Mailchimp's privacy practices.
            </p>
          </div>
        </div>
        <div hidden="">
          <input type="hidden" name="tags" value="3248529,4058414" />
        </div>
        <div id="mce-responses" class="clear">
          <div
            class="response"
            id="mce-error-response"
            style="display: none"
          ></div>
          <div
            class="response"
            id="mce-success-response"
            style="display: none"
          ></div>
        </div>
        <div aria-hidden="true" style="position: absolute; left: -5000px">
          <input
            type="text"
            name="b_45feb84423dd88462feb155c0_89976dbaa5"
            tabindex="-1"
            value=""
          />
        </div>
        <div class="clear">
          <input
            type="submit"
            name="subscribe"
            id="mc-embedded-subscribe"
            class="button"
            value="Subscribe"
          />
        </div>
      </div>
    </form>
  </div>
  <script
    type="text/javascript"
    src="//s3.amazonaws.com/downloads.mailchimp.com/js/mc-validate.js"
  ></script>
</div>


## Contact

Challenge mail: [challenge.confiance@irt-systemx.fr](mailto:challenge.confiance@irt-systemx.fr)

Discord: [European Trustworthy AI Foundation #welding-quality-detection-challenge](https://discord.gg/G9RhAECmVr)

<br>
<br>
<br>
<br>
<br>