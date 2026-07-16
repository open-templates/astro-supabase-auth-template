<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";
import { Loader2 } from "lucide-vue-next";
import { useAuth } from "@/vue/composables/useAuth";
import { fetchMe, type MeResponse } from "@/vue/api/me";
import UiCard from "@/vue/components/ui/UiCard.vue";
import UiCardContent from "@/vue/components/ui/UiCardContent.vue";
import UiCardDescription from "@/vue/components/ui/UiCardDescription.vue";
import UiCardHeader from "@/vue/components/ui/UiCardHeader.vue";
import UiCardTitle from "@/vue/components/ui/UiCardTitle.vue";

const { user } = useAuth();
const profile = ref<MeResponse | null>(null);
const loading = ref(true);
const error = ref<string | null>(null);

let cancelled = false;

onMounted(async () => {
  loading.value = true;
  error.value = null;
  const { data, error: apiError } = await fetchMe();
  if (cancelled) return;
  if (apiError || !data) {
    error.value = apiError ?? "Failed to load profile";
    profile.value = null;
  } else {
    profile.value = data;
  }
  loading.value = false;
});

onUnmounted(() => {
  cancelled = true;
});
</script>

<template>
  <div class="flex flex-col gap-6 py-8">
    <div>
      <h1 class="text-3xl font-bold tracking-tight">Welcome</h1>
      <p class="text-muted-foreground mt-1">
        You are signed in. This page calls the protected
        <code class="text-sm">GET /me</code> API on your Cloudflare Worker backend.
      </p>
    </div>

    <UiCard>
      <UiCardHeader>
        <UiCardTitle>Session (Supabase client)</UiCardTitle>
        <UiCardDescription>From the browser Supabase auth session.</UiCardDescription>
      </UiCardHeader>
      <UiCardContent class="space-y-1 text-sm">
        <p><span class="text-muted-foreground">Email:</span> {{ user?.email }}</p>
        <p><span class="text-muted-foreground">User ID:</span> {{ user?.id }}</p>
      </UiCardContent>
    </UiCard>

    <UiCard>
      <UiCardHeader>
        <UiCardTitle>Profile (API /me)</UiCardTitle>
        <UiCardDescription>
          Returned by cf-hono-supabase-api-template using your JWT.
        </UiCardDescription>
      </UiCardHeader>
      <UiCardContent>
        <div v-if="loading" class="flex items-center gap-2 text-sm text-muted-foreground">
          <Loader2 class="h-4 w-4 animate-spin" />
          Loading profile…
        </div>
        <p v-else-if="error" class="text-sm text-destructive">{{ error }}</p>
        <pre v-else class="overflow-x-auto rounded-md bg-muted p-4 text-xs">{{
          JSON.stringify(profile, null, 2)
        }}</pre>
      </UiCardContent>
    </UiCard>
  </div>
</template>
