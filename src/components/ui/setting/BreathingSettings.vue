<template>
  <div class="mx-auto max-w-[50%]">
    <Breather is-preview />
  </div>
  <!-- prettier-ignore -->
  <Setting
    :key="settingBs.id"
    v-bind="(settingBs as any)"
    is-decimal
  />

  <!-- prettier-ignore -->
  <Setting
    v-for="setting in settingsDefaults"
    :key="setting.id"
    v-bind="(setting as any)"
    class="mt-4"
  />
  <Button
    size="lg"
    variant="secondary"
    class="mt-3 w-full"
    @click="resetBreathingSettings"
  >
    Restore defaults
  </Button>
</template>

<script setup lang="ts">
import Breather from "@/components/ui/breather/Breather.vue";
import Setting from "@/components/ui/setting/Setting.vue";
import Button from "@/components/ui/button/Button.vue";
import useBreathingSession from "@/composables/useBreathingSession";

const { resetBreathingSettings } = useBreathingSession();

interface SettingDefinition {
  id: string;
  label: string;
  min: number;
  max: number;
  step?: number;
}

const settingBs: SettingDefinition = {
  id: "breathingSpeed",
  label: "Breathing Speed",
  min: 25,
  max: 55,
  step: 1,
};

const settingsDefaults: SettingDefinition[] = [
  {
    id: "breaths",
    label: "Breaths",
    min: 10,
    max: 100,
    step: 5,
  },
  {
    id: "rounds",
    label: "Rounds",
    min: 1,
    max: 10,
  },
  {
    id: "pauseBetweenRounds",
    label: "Pause between Rounds",
    min: 0,
    max: 30,
    step: 5,
  },
  {
    id: "pauseBeforeFirstRound",
    label: "Pause before First Round",
    min: 0,
    max: 30,
    step: 5,
  },
  {
    id: "holdAfterInhale",
    label: "Hold after Inhale",
    min: 5,
    max: 30,
    step: 5,
  },
];
</script>

<style scoped></style>
