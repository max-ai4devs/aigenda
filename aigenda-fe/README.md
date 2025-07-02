# Vue 3 + TypeScript + Vite + Tailwind CSS 4

## Initial setup
1. Create a new Vue 3 project with Vite:
```bash
pnpm create vite@latest
# name: aigenda-fe
# framework: Vue
# variant: Typescript

cd aigenda-fe
pnpm install
# pnpm run dev
```


2. Install and integrate Tailwind CSS 4:

  - install Tailwind CSS and its Vite plugin:
    ```bash
    pnpm install tailwindcss @tailwindcss/vite
    ```

  - update `/aigenda/aigenda-fe/vite.config.ts`:
    ```ts
    import tailwindcss from '@tailwindcss/vite'
    // ...
    plugins: [vue(), tailwindcss()],
    // ...
    ``` 

  - replace content of `/aigenda/aigenda-fe/src/style.css` with:
    ```css
    @import 'tailwindcss';
    ```


3. Use Tailwind CSS in your components:

  For instance update `/aigenda/aigenda-fe/src/components/HelloWorld.vue`:
    ```vue
    <template>
      <h1 class="text-2xl font-bold bg-green-500">{{ msg }}</h1>
    </template>

    <script setup lang="ts">
    defineProps<{ msg: string }>()
    </script>
    ```

## Recommended Extensions
See ../.vscode/extensions.json for recommended VS Code extensions.


This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

Learn more about the recommended Project Setup and IDE Support in the [Vue Docs TypeScript Guide](https://vuejs.org/guide/typescript/overview.html#project-setup).
