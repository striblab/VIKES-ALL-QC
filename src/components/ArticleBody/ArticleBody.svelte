<script>
  import Grid from '../Grid/Grid.svelte';
  import GridRow from '../Grid/_GridRow.svelte';
  import Subhead from './_Subhead.svelte';
  import Paragraph from './_Paragraph.svelte';
  import Cards from './_Cards.svelte';
  import Image from '../Image/Image.svelte';
  import ScrollySection from '../Scrolly/ScrollySection.svelte';

  let innerWidth = $state(0);
  let isMobile = $derived(innerWidth < 768);
  let isTablet = $derived(innerWidth >= 768 && innerWidth < 1024);
  let isDesktop = $derived(innerWidth >= 1024);
</script>

<svelte:window bind:innerWidth />

<Grid additionalClasses={'gap-y-0'}>
  <GridRow variant={'inline'} additionalClasses={'gap-y-5 pt-2 pb-6'}>
    <Paragraph
      >From no-brainer consensus picks to choosing three different quarterbacks
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

  <GridRow
    additionalClasses="justify-self-center text-center w-[60%] mx-auto pt-12 pb-8"
  >
    <hr style="border-width: 2px;border-color: #ffb601 !important;" />
    <div
      style="
margin: -45px auto auto auto;
max-width: 85px;
background: white;
padding: 10px;
"
    >
      <img
        src="https://static.startribune.com/news/projects/all/2025-VIKES-ALLQC/png%20assets/purple%20logo1.png"
      />
    </div>
  </GridRow>

  <GridRow variant={'fullBleed'}>
    <div class="leadertext">STAR TRIBUNE VIKINGS ALL-QUARTER CENTURY</div>
    <div class="toggler">
      Offense&nbsp;&nbsp;&nbsp;&nbsp;<b>|</b
      >&nbsp;&nbsp;&nbsp;&nbsp;Defense&nbsp;&nbsp;&nbsp;&nbsp;<b>|</b
      >&nbsp;&nbsp;&nbsp;&nbsp;Special Teams/Coach
    </div>
    <Cards />
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

<style>
</style>
