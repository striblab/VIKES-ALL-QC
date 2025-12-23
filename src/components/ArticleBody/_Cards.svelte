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

  // manage the flip state

  const isTouch =
    typeof window !== 'undefined' &&
    ('ontouchstart' in window || navigator.maxTouchPoints > 0);
  let flippedId = null;
  function onEnter(id) {
    if (!isTouch) flippedId = id;
  }
  function onLeave(id) {
    if (!isTouch && flippedId === id) flippedId = null;
  }
  function onTap(id) {
    if (!isTouch) return;
    flippedId = flippedId === id ? null : id;
  }
</script>

<div class="my-4 card-list max-w-[1800px] gap-9 flex flex-row flex-wrap px-4 mx-auto justify-center">
  {#each items as item, i (i)}
    {#if item.winner}
      <button
          type="button"
          class="card w-[270px] h-[379px] relative mt-8 bg-none p-0 text-left border-0 card-{items.indexOf(item) + 1} {getGroupClass(
            item.group,
          )} cursor-pointer perspective-[1000px]"
          class:flip={flippedId === i}
          aria-pressed={flippedId === i}
          aria-label="Flip card for {item.name}"
          on:mouseenter={() => onEnter(i)}
          on:mouseleave={() => onLeave(i)}
          on:click={() => onTap(i)}
          on:keydown={(e) => {
            if (e.key === 'Enter' || e.key === ' ') {
              e.preventDefault();
              onTap(i);
            }
          }}
      >
        <div class="text-center absolute -top-[30px] w-full font-[Graphik-semibold] uppercase text-[1rem] pb-2">
          {item.position}
        </div>
        <div class="card-content relative w-full h-full">
          <div title="Image of our {item.name} player card." class="card-front shadow-[10px_10px_20px_-5px_rgba(0,0,0,.5)] absolute w-full h-full p-0 bg-no-repeat bg-cover bg-center" style="background-image:url('https://ststatic.stimg.co/news/projects/all/2025-VIKES-ALLQC/card-finals/{item.image_url}?w=540')"></div>
          <div class="card-back shadow-[10px_10px_20px_-5px_rgba(0,0,0,.5)] absolute w-full h-full font-[Graphik-regular] card-{item.position}">
            <div class="cardback-content relative bg-cover w-full h-full bg-[url('https://ststatic.stimg.co/news/projects/all/2025-VIKES-ALLQC/img/cardback-122125-2.png?w=540')]">
              <div class="card-back-body pt-[9%] mx-auto h-full">
                <div class="nameplate pb-[6px] text-center font-[Graphik-bold] text-[1.25rem] leading-[90%]">
                  {#if item.position != "Flex"}
                    {item.name}
                  {/if}
                  {#if item.position == "Flex"}
                    {@html item.flex_winners}
                  {/if}
                </div>
                {#if item.position != "Flex"}
                  <div class="posinfo text-center text-[.85rem]">
                    <span class="name font-[Graphik-semibold] text-[#4f2683]">{item.position}</span>
                    <span class="jersey_num">#{item.jersey_number} &#8226; </span>
                    <span class="years">{item.years}</span>
                  </div>
                {/if}
                <div class="blurb relative z-10 font-[Graphik-regular] text-[.9rem] overflow-scroll overflow-x-hidden h-full max-h-[68%] mt-[17%] mr-[3.75%] ml-[3.75%]">
                  <div class="blurb-text pl-4 pr-4 leading-[1.15rem] -tracking-[.25px]">
                    {@html item.blurb}
                    <div class="attrib text-right mt-[.5rem]">
                      {#if item.position != "Flex"}
                        &mdash; <span class="font-[Graphik-semibold]">{item.blurb_author}</span>
                      {/if}
                    </div>
                    
                    <div class="other_voters pt-2 pb-4">
                      <h3>Vote results:</h3>
                      {#if !item.other_votes}
                        ❎ ❎ ❎ Unanimous
                      {/if}
                      {#if item.other_votes}
                        {@html item.other_votes}
                      {/if}
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="fadedScroller_fade z-20 h-[1.5rem] w-full absolute bottom-[6.2773%] pr-[8%] pl-[8%]">
              <div class="h-full bg-[linear-gradient(to_bottom,rgba(251,251,251,0)_0%,rgba(255,251,238,1)_100%)]"></div>
            </div>
          </div>
        </div>
      </button>
    {/if}
  {/each}
</div>
<style></style>
