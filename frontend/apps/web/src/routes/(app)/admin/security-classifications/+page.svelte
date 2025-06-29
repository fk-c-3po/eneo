<!--
    Copyright (c) 2024 Sundsvalls Kommun

    Licensed under the MIT License.
-->

<script lang="ts">
  import { Page, Settings } from "$lib/components/layout";
  import MultipleModelsClassificationDialog from "$lib/features/security-classifications/components/MultipleModelsClassificationDialog.svelte";
  import SecurityClassificationEnabledSetting from "$lib/features/security-classifications/components/SecurityClassificationEnabledSetting.svelte";
  import SecurityClassificationListSetting from "$lib/features/security-classifications/components/SecurityClassificationListSetting.svelte";
  import { initSecurityClassificationService } from "$lib/features/security-classifications/SecurityClassificationsService.svelte.js";

  const { data } = $props();

  initSecurityClassificationService(data.intric, data.securityClassifications);
  // Using a JS string so we can have a newline in this
  const description =
    "Select a security classification for all of you organisation's models.\nModels will be available in spaces with the same or lower classification.";
</script>

<svelte:head>
  <title>Eneo.ai – Admin – Security classifications</title>
</svelte:head>

<Page.Root>
  <Page.Header>
    <Page.Title title="Security"></Page.Title>
  </Page.Header>
  <Page.Main>
    <Settings.Page>
      <Settings.Group title="General">
        <SecurityClassificationEnabledSetting></SecurityClassificationEnabledSetting>
      </Settings.Group>
      <Settings.Group title="Configuration">
        <SecurityClassificationListSetting></SecurityClassificationListSetting>

        <Settings.Row title="Classify models" {description} fullWidth>
          <div class="grid gap-4">
            <MultipleModelsClassificationDialog
              models={data.models.completionModels}
              type="completionModel"
            ></MultipleModelsClassificationDialog>
            <MultipleModelsClassificationDialog
              models={data.models.embeddingModels}
              type="embeddingModel"
            ></MultipleModelsClassificationDialog>
            <MultipleModelsClassificationDialog
              models={data.models.transcriptionModels}
              type="transcriptionModel"
            ></MultipleModelsClassificationDialog>
          </div>
        </Settings.Row>
      </Settings.Group>
    </Settings.Page>
  </Page.Main>
</Page.Root>
