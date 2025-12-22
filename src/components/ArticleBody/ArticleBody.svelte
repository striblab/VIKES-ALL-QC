<script>
  import Grid from '../Grid/Grid.svelte';
  import GridRow from '../Grid/_GridRow.svelte';
  import Paragraph from './_Paragraph.svelte';
  import Cards from './_Cards.svelte';

  let innerWidth = $state(0);
  let isMobile = $derived(innerWidth < 768);
  let isTablet = $derived(innerWidth >= 768 && innerWidth < 1024);
  let isDesktop = $derived(innerWidth >= 1024);

  const groups = [
    { label: 'Offense', className: 'offenseGroup' },
    { label: 'Defense', className: 'defenseGroup' },
    { label: 'ST/Coach', className: 'specialteamsGroup' }
  ];

  let activeGroup = $state(groups[0].className);
  let groupClass = $derived(activeGroup); // tracks the active button click

  function setGroup(next) {
    activeGroup = next;
  }

  // sticky card nav support

  import { onMount } from 'svelte';
  let headerOffset = $state(0);
  function updateCardNavOffset() {
    const header = document.getElementById('global-header');
    if (!header) return;
    headerOffset = header.offsetHeight;
  }
  $effect(() => {
    updateCardNavOffset();
    window.addEventListener('resize', updateCardNavOffset);
    return () => window.removeEventListener('resize', updateCardNavOffset);
  });
  function observeCardNav() {
    const el = document.getElementById('cardNav');
    if (!el) return;
    const offset = headerOffset;
    const checkPosition = () => {
      const { top } = el.getBoundingClientRect();

      if (top <= offset) {
        el.classList.add('stuck');
      } else {
        el.classList.remove('stuck');
      }
    };
    window.addEventListener('scroll', checkPosition, { passive: true });
    window.addEventListener('resize', checkPosition);

    return () => {
      window.removeEventListener('scroll', checkPosition);
      window.removeEventListener('resize', checkPosition);
    };
  }
  onMount(() => {
    const cleanup = observeCardNav();
    return cleanup;
  });

</script>

<svelte:window bind:innerWidth />

<Grid additionalClasses={'gap-y-0'}>
  <GridRow variant={'inline'} additionalClasses={'gap-y-5 pt-2 pb-6'}>
    
    <Paragraph
      ><p class="drop-cap font-[publico-headline-black] float-left leading-none text-[76px] pr-2 relative -top-[2px] h-[50px]">F</p>rom no-brainer consensus picks to choosing three different quarterbacks
      and three different head coaches, the Minnesota Star Tribune’s Ben
      Goessling, Andrew Krammer and Mark Craig have used a combined half-century
      of experience covering the Vikings to assemble their versions of what the
      Purple’s All-Quarter Century team should look like.</Paragraph
    >

    <Paragraph>Let the second-guessing and back-biting begin!</Paragraph>

    <Paragraph
      >Goessling (Year 14), Krammer (13) and Craig (23) were asked to pick 27
      players – 11 on offense, 11 on defense and five specialists – and a head
      coach who were with the Vikings from the 2000 season to the present. The
      players and coaches were selected based on only those seasons they spent
      with the Vikings.</Paragraph
    >

    <Paragraph
      >The offense includes two receivers, one running back, one tight end and a
      “flex” option that led to three different choices of skill players. The
      five linemen are position specific.</Paragraph
    >

    <Paragraph
      >The defense includes two tackles, two edge rushers, two linebackers, two
      safeties and three corners, one of them a nickel back.</Paragraph
    >
    
    <Paragraph>
      <iframe style="aspect-ratio: 16 / 9;width:100%;max-width:1080px;margin:auto;" src="https://www.youtube.com/embed/1FxJUubvDCc" title="YouTube video player" frameborder="0" allow="picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
      <div class="rt-Box mt-2 font-utility-meta-reg-02 text-text-secondary col-span-full ArticleHero_leadart-standard-credit__Y1_wU">Ben Goessling and Emily Leiker discuss both the off-field and on-field happenings from the Vikings trip to face the Giants at MetLife Stadium, including plane troubles out of MSP and injuries to J.J. McCarthy and others. Plus, they discuss big performances by Justin Jefferson and Aaron Jones Sr., and how Max Brosmer fared helming the offense through the second half.</div>
    </Paragraph>

    <Paragraph
      >The Strib’s trio passed the first competency test by making Pro Football
      Hall of Famers Randy Moss, Steve Hutchinson and Jared Allen three of their
      19 unanimous choices. They also aced the second competency exam by
      agreeing on four players – Adrian Peterson, Justin Jefferson, Harrison
      Smith and Kevin Williams – who are likely on their way to Canton (Peterson
      as early as 2027 and Jefferson), currently a candidate (Williams) or will
      be given serious consideration (Smith).</Paragraph
    >

    <Paragraph
      >Throw in nickel back Antoine Winfield, kick returner Cordarrelle
      Patterson, punt returner Marcus Sherels and linebackers Chad Greenway and
      Eric Kendricks as other no-brainers.</Paragraph
    >

    <Paragraph
      >Four of the consensus picks are current Vikings players — Jefferson,
      Smith, Brian O’Neill and Byron Murphy Jr.</Paragraph
    >

    <Paragraph
      >The three selectors disagreed on very little. Craig liked second-year
      kicker Will Reichard by a nose — and a very strong toe — over Ryan
      Longwell, the pick of the other two. And Goessling and Craig like current
      long-snapper Andrew DePaola over Krammer’s choice, Cullen Loeffler
      (2004-14).</Paragraph
    >

    <Paragraph
      >But at two key positions, they disagreed quite a bit: Goessling, Krammer
      and Craig chose three different coaches and three different quarterbacks,
      speaking volumes as to why the first 25 years of this century have been
      consistently inconsistent. In those cases, we had readers vote to break
      the tie.</Paragraph
    >

    <Paragraph
      >The Vikings missed the playoffs more times (15) than they made it (10)
      and appeared in back-to-back postseasons only once (2008-09). They played
      in 15 playoff games, going 5-10 with eight different quarterbacks – Daunte
      Culpepper, Tarvaris Jackson, Brett Favre, Joe Webb, Teddy Bridgewater,
      Case Keenum, Kirk Cousins and Sam Darnold – and six different coaches –
      Denny Green, Mike Tice, Brad Childress, Leslie Frazier, Mike Zimmer and
      Kevin O’Connell.</Paragraph
    >

    <Paragraph
      >So which QB and coach would you pick to lead your Vikings All-Quarter
      Century team? Goessling went with Daunte Culpepper and Mike Zimmer.
      Krammer likes Kirk Cousins and current coach Kevin O’Connell. And Craig
      couldn’t help but invite a gunslinging Cheesehead to the party by
      reuniting Brett Favre with Brad Childress.</Paragraph
    >

    <Paragraph
      >Like we said, let the second-guessing and back-biting begin!</Paragraph
    >
  </GridRow>

  <GridRow additionalClasses="justify-self-center text-center w-[80%] md:w-[60%] mx-auto pt-8 pb-8">
    <hr class="border-[#ffb601] border-[1px]">
    <div class="bg-white w-[60px] relative -mt-[23px] mx-auto px-2">
      <img class="w-[60px] mx-auto" alt="Star Tribune Star" src="https://ststatic.stimg.co/news/projects/all/2025-VIKES-ALLQC/img/strib-star.png?w=120">
    </div>
  </GridRow>

  <GridRow variant={'fullBleed'}>
    <div class="leadertext font-[Graphik-bold] uppercase text-center text-[1.5rem] mx-auto leading-[120%] pb-4 -tracking-[1px]">Minnesota Star Tribune<br>Vikings all-quarter century</div>
    
    <!-- print the nav buttons -->

    <div id="cardNav" style={`top:${headerOffset}px`} class="toggler px-4 py-4 text-[1rem] leading-[100%] md:text-[1.15em] text-center mx-auto font-[Graphik-regular] letterspacing-[2px] sticky z-20 bg-[white]">
      {#each groups as g}
        <button
          type="button"
          class="px-4 py-1 uppercase"
          class:active={activeGroup === g.className}
          on:click={() => setGroup(g.className)}
        >
          {g.label}
        </button>
      {/each}
    </div>

    <div id="cardGroups" class={groupClass}>
      <Cards />
    </div>
  </GridRow>
</Grid>
<Grid additionalClasses={'gap-y-0'}>
  <GridRow variant={'inline'} additionalClasses={'gap-y-5 pt-8'}>
    <div class="credits text-center mb-8 rt-Box font-utility-meta-reg-02 text-text-secondary col-span-full ArticleHero_leadart-standard-credit__Y1_wU mt-[6px] px-4">
      <p class="pb-[3px]"><span class="font-[Graphik-semibold]">Design and development:</span> Joe Rull and Jamie Hutt</p>
      <p><span class="font-[Graphik-semibold]">Editing:</span> Naila-Jean Meyers and Kenneth Chia</p>
</div>
  </GridRow>
</Grid>
<!-- 
@component
### ArticleBody component
This is a general workspace illustrating what an article body might look like if you use only the components included in this template.  
ArticleBody doesn't accept any props. All contents will need to be hand-placed by a designer directly inside this component.  
In this example, Grid and GridRow help establish the width of the article body's contents. 
Documentation included with those components and accessed by VSCode tooltip explains each component in greater detail.

#### State in this component
- innerWidth: int - pixel width of the viewport.
- isMobile: boolean - derived from innerWidth, true if less than 768 pixels
- isTablet: boolean - derived from innerWidth, true if between 768 pixels inclusive and 1024 pixels exclusive
- isDesktop: boolean - derived from innerWidth, true if greater than 1024 pixels inclusive

#### Using state in this component
You can use any of the three derived states to render different variants of a GridRow component reactively.
The following example uses a ternary to render an image edge-to-edge on mobile but inline otherwise.

#### Example
```svelte
  <GridRow
    variant={isMobile ? "fullBleed" : "inline"}
  >
    <Image
      src="https://arc.stimg.co/startribunemedia/4SPNT7DI36ANT2SOB5N5EJAIJU.jpg"
      alt="Descriptive alt text"
      caption="Caption tk tk tk"
    />
  </GridRow>
```
-->

<style></style>
