<script>
  import { createEventDispatcher, onMount } from 'svelte';
  const DATA_URL =
    'https://static.startribune.com/news/projects/all/2025-VIKES-ALLQC/data.json';
  let items = [];
  let loading = true;
  let error = '';
  let groupClass = '';

  onMount(async () => {
    try {
      const res = await fetch(DATA_URL);
      if (!res.ok) throw new Error(`HTTP ${res.status}`);
      const json = await res.json();
      if (!Array.isArray(json))
        throw new Error('Unexpected data format (expected array).');
      items = json;
      // console.log('FIRST ROW SAMPLE:', items[0], Object.keys(items[0] || {}));
    } catch (e) {
      error = e?.message || String(e);
    } finally {
      loading = false;
    }
  });

  // some helpers

  function getGroupClass(group) {
    if (group === 'Offense') return 'offense';
    if (group === 'Defense') return 'defense';
    return 'specialteams';
  }
</script>

<div
  class="card-list max-w-[1800px] flex flex-row flex-wrap p-0 m-auto justify-center"
>
  {#each items as item}
  {#if item.winner}
    <div
      class="card card-{items.indexOf(item) + 1} {getGroupClass(
        item.group,
      )} cursor-pointer p-0 pb-8 aspect-[1750/2457] bg-transparent perspective-[1000px]"
    >
      <div class="poslabel">{item.position}</div>
      <div class="card-content relative w-full h-full">
        <div
          class="card-front absolute w-full h-full bg-no-repeat bg-cover bg-center p-0"
          style="background-image:url('https://static.startribune.com/news/projects/all/2025-VIKES-ALLQC/img/{item.image_url}');"
        ></div>
        <div class="card-back absolute w-full h-full">
          <div
            class="cardback-content relative aspect-[1750/2457] bg-cover w-full h-full bg-[url('https://static.startribune.com/news/projects/all/2025-VIKES-ALLQC/img/cardback.png')]"
          >
            <div class="card-header">
              <div class="nameplate pb-2">{item.name}</div>
              <div class="posinfo pb-1">
                <span class="name" style="font-weight:bold; color: #4f2683">{item.position}</span>
                <span class="jersey_num">#{item.jersey_number} &#8226; </span>
                <span class="years">{item.years}</span>
              </div>
              <div class="blurb">
                <span class="blurb-text">{item.blurb}</span>
                <div class="attrib pb-1">&mdash; <b>{item.blurb_author}</b></div>
                <div class="other_voters pt-2 pb-8"
                  >Also recieving votes:<br />{@html item.other_votes}</div
                >
              </div>
              <div class="fadedScroller_fade"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
    {/if}
  {/each}
</div>

<style></style>
