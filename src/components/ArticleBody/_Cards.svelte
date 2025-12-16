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
  class="card-list max-w-[1500px] flex flex-row flex-wrap p-0 m-auto justify-center"
>
  {#each items as item}
    <div
      class="card card-{items.indexOf(item) + 1} {getGroupClass(
        item.group,
      )} cursor-pointer p-0 pb-8 aspect-[1750/2457] min-w-[15vw] bg-transparent perspective-[1000px]"
    >
      <div class="poslabel">{item.position}</div>
      <div class="card-content relative w-full h-full">
        <div
          class="card-front absolute w-full h-full bg-no-repeat bg-contain bg-center p-0"
          style="background-image:url('https://static.startribune.com{item.image_url}');"
        ></div>
        <div class="card-back absolute w-full h-full">
          <div
            class="cardback-content relative aspect-[1750/2457] bg-cover w-full h-full bg-[url('https://static.startribune.com/news/projects/all/2025-VIKES-ALLQC/img/cardback.png')]"
          >
            <div class="card-header">
              <div class="nameplate">{item.name}</div>
              <div class="posinfo">
                <span class="name">{item.position}</span>
                <span class="jersey_num">{item.jersey_number}</span>
                <span class="years">{item.years}</span>
              </div>
            </div>
            <div class="blurb">
              <span class="blurb-text">{item.blurb}</span>
              <span class="attrib">&mdash; {item.blurb_author}</span>
              <span class="other_voters"
                >Also recieving votes:<br />{item.other_votes}</span
              >
            </div>
            <div class="fadedScroller_fade"></div>
          </div>
        </div>
      </div>
    </div>
  {/each}
</div>

<style></style>
