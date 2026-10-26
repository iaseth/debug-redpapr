<script lang="ts">
	const events = $state<KeyboardEvent[]>([]);

	function onkeydown (e: KeyboardEvent) {
		events.push(e);
	}
</script>

<svelte:window {onkeydown} />

<section class="text-center p-4 py-12">
	<h1>Press any key</h1>
</section>

<section class="overflow-x-auto p-4">
	{#if events.length > 0}
		<table class="table table-zebra table-sm whitespace-nowrap">
			<thead>
				<tr>
					<th>#</th>
					<th>Key</th>
					<th>Code</th>
					<th>Location</th>
					<th>Repeat</th>
					<th>Ctrl</th>
					<th>Alt</th>
					<th>Shift</th>
					<th>Meta</th>
					<th>Time</th>
				</tr>
			</thead>

			<tbody>
				{#each events as event, i}
					<tr>
						<td>{i + 1}</td>
						<td class="font-mono font-bold">{event.key}</td>
						<td class="font-mono">{event.code}</td>
						<td>{event.location}</td>
						<td>{event.repeat ? '🔁' : '—'}</td>
						<td>{event.ctrlKey ? '✅' : '—'}</td>
						<td>{event.altKey ? '✅' : '—'}</td>
						<td>{event.shiftKey ? '✅' : '—'}</td>
						<td>{event.metaKey ? '✅' : '—'}</td>
						<td class="font-mono">{event.timeStamp.toFixed(3)} ms</td>
					</tr>
				{/each}
			</tbody>
		</table>
	{/if}
</section>