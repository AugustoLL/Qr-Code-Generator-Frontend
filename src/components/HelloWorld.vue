<template>
  <v-container class="fill-height">
    <v-responsive
      class="align-centerfill-height mx-auto"
      max-width="900"
    >

      <div class="text-center">
        <h1 class="text-h2 font-weight-bold">QR Code Generator</h1>
      </div>

      <div class="py-4"></div>

      <v-row>
        <v-col cols="6">
          <v-card
            class="py-4"
            color="secondary"
            rounded="lg"
            variant="outlined"
          >
          <v-card-title>Let's make a QR Code!</v-card-title>
          <v-card-subtitle>Complete the following form:</v-card-subtitle>
            <v-form>
              <v-container>
                <v-row>
                  <v-text-field
                    class="mb-2 mx-4"
                    :v-model="URL.value"
                    prepend-icon="mdi-link-variant"
                    label="URL"
                    :rules="URL.rules"
                    hide-details="auto"
                    type="url"
                  ></v-text-field>
                </v-row>
                <v-card-title>Format</v-card-title>
                <v-row>
                  <v-chip-group
                    :v-model="FORMAT.value"
                    class="mb-2 mx-4"
                    prepend-icon="mdi-image"
                    label="Format"
                    :rules="FORMAT.rules"
                    hide-details="auto"
                    mandatory
                  >
                  <v-chip 
                    v-for="format in FORMATS"
                    :key="format"
                    :text="format"
                    :value="format"
                    variant="outlined" 
                    filter
                  ></v-chip>
                </v-chip-group>
                </v-row>
              </v-container>
            </v-form>
          </v-card>
        </v-col>

        <v-col cols="6">
          <v-card
            class="py-4 px-4"
            color="primary"
            rounded="lg"
            variant="outlined"
          >
            <v-img
            rounded="lg"
            position="center"
            src="https://github.com/AugustoLL/Qr-Code-Generator-Backend/raw/main/examples/youtubeQRCode.png"
            ></v-img>

            <v-btn variant="outlined" color="primary" class="mt-4">
              Generate
            </v-btn>

            <template #title>
              <h2 class="text-h5 font-weight-bold">Preview</h2>
            </template>

            <template #subtitle>
              <div class="text-subtitle-1">
                Change this page by updating <v-kbd>{{ `<HelloWorld />` }}</v-kbd>.
              </div>
            </template>
            <v-overlay
              opacity=".06"
              scrim="primary"
              contained
              model-value
              persistent
            />
          </v-card>
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script setup lang="ts">
  const URL = {
    value: '',
    rules: [
      (value: string) => !!value || 'This field is required.',
      (value: string) => value.length <= 2000 || 'Max 2000 characters',
      (value: string) => {
        const pattern = /^https?:\/\/(?:www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b(?:[-a-zA-Z0-9()@:%_\+.~#?&\/=]*)$/;
        return pattern.test(value) || 'Invalid URL.'
      },
    ],
  };
  const FORMAT = {
    value: 'png',
    rules: [
      (value: string) => !!value || 'This field is required.',
      (value: string) => ('png' || 'jpg' || 'jpeg') === value || 'Invalid format.',
    ],
  };
  const FORMATS = ['png', 'jpg', 'jpeg'];
</script>
