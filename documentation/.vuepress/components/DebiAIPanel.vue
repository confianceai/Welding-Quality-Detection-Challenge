<template>
  <div id="bg1">
    <div id="bg2">
      <a href="https://debiai.irt-systemx.fr/" target="_blank">
        <img
          src="https://debiai.irt-systemx.fr/logo_debiai.png"
          alt="DebiAI Logo"
          class="debiai-logo"
        />
      </a>
      <p>
        <strong>DebiAI</strong> is an open-source <b>bias detection</b> and
        <b>contextual evaluation</b> tool for AI projects.
        <br />
        We used it to explore the
        <i>Welding Detection Challenge Dataset Metadata </i> parquet file:
      </p>
      <img
        src="https://raw.githubusercontent.com/debiai/use-cases/main/weldingQuality/images/MetadataAnalysis.png"
        alt="Dataset analysis DebiAI dashboard"
        class="dataset-analysis-img"
      />
      <p>
        <a href="https://demo.debiai.fr/#/" target="_blank" class="analyze-link"
          >Analyze the challenge dataset on our public DebiAI instance</a
        >
      </p>
      <div class="spacer"></div>
      <p>
        DebiAI was designed to assist data scientists in exploring datasets like
        the one described in this challenge.
        <br />
        <a
          href="https://github.com/debiai/use-cases/blob/main/weldingQuality/README.md"
          target="_blank"
          class="create-project-link"
          >How to create your own Challenge Dataset DebiAI project</a
        >
      </p>
      <p class="footer">
        DebiAI is developed by
        <a href="https://www.irt-systemx.fr/" title="IRT SystemX">
          <img
            src="https://www.irt-systemx.fr/wp-content/uploads/2013/03/system-x-logo.jpeg"
            class="irt-logo"
          />
        </a>
        And is integrated in
        <a href="https://www.confiance.ai/" title="Confiance.ai">
          <img
            src="https://pbs.twimg.com/profile_images/1443838558549258264/EvWlv1Vq_400x400.jpg"
            class="confiance-logo"
          />
        </a>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "DebiAIPanel",
};
</script>

<style scoped lang="stylus">
#bg1 {
  background: linear-gradient(45deg, #31b7bc, #009ddf);
  padding: 15px;
  border-radius: 40px;

  #bg2 {
    background: white;
    border-radius: 30px;
    text-align: center;
    padding: 20px;

    .debiai-logo {
      width: 150px;
    }

    .dataset-analysis-img {
      max-width: 80%;
      border-radius: 20px;
      margin-top: 10px;
    }

    .analyze-link {
      color: #009ddf;
      font-weight: bold;
    }

    .spacer {
      margin-top: 8px;
    }

    .create-project-link {
      color: #009ddf;
      text-decoration: none;
    }

    .footer {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 10px;
      flex-wrap: wrap;

      .irt-logo,
      .confiance-logo {
        height: 70px;
      }
    }
  }
}
</style>
