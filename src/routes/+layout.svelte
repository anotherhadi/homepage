<script lang="ts">
	import '../app.css';
	import '../fonts.css';
	import { ModeWatcher } from 'mode-watcher';
	import { config } from './config.json';
</script>

<ModeWatcher />
<div class="h-full w-full" style="background-color: {config.colors.background};">
	<div class="relative mx-auto min-h-screen max-w-4xl p-10">
		<slot></slot>
	</div>
</div>
