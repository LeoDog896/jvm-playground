<script lang="ts">
	import * as monaco from 'monaco-editor';
	import { onMount } from 'svelte';

    let container: HTMLDivElement;
    export let language: string;
    export let value: string;

    onMount(() => {
        (globalThis as any).MonacoEnvironment = {
            getWorker: function (workerId: any, label: any) {
                const getWorkerModule = (moduleUrl: any, label: any) => {
                    return new Worker((globalThis as any).MonacoEnvironment.getWorkerUrl(moduleUrl), {
                        name: label,
                        type: 'module'
                    });
                };

                switch (label) {
                    case 'json':
                        return getWorkerModule('/monaco-editor/esm/vs/language/json/json.worker?worker', label);
                    case 'css':
                    case 'scss':
                    case 'less':
                        return getWorkerModule('/monaco-editor/esm/vs/language/css/css.worker?worker', label);
                    case 'html':
                    case 'handlebars':
                    case 'razor':
                        return getWorkerModule('/monaco-editor/esm/vs/language/html/html.worker?worker', label);
                    case 'typescript':
                    case 'javascript':
                        return getWorkerModule(
                            '/monaco-editor/esm/vs/language/typescript/ts.worker?worker',
                            label
                        );
                    default:
                        return getWorkerModule('/monaco-editor/esm/vs/editor/editor.worker?worker', label);
                }
            }
        };

        monaco.editor.create(container, {
            value,
            language
        });
    })
</script>

<div bind:this={container}></div>

<style>
    div {
        width: 100%;
        height: 100%;
    }
</style>