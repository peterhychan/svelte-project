<script>
  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import TextInput from "./UI/TextInput.svelte";
  import Button from "./UI/Button.svelte";
  import EditMeetup from "./Meetups/EditMeetup.svelte";

  let meetups = [
    {
      id: "e1",
      title: "Paint SF",
      subtitle: "May the ART to be with you",
      description: "May the ART to be with you",
      imageUrl:
        "https://cdn.shopify.com/s/files/1/1136/0164/products/sanfran_grande.jpg?v=1459449289",
      address: "123 Poke Street, San Francisco, CA 94105",
      contact: "painsf@test.com",
      isFavorite: false
    },
    {
      id: "e2",
      title: "Paint SF",
      subtitle: "May the ART to be with you",
      description: "May the ART to be with you",
      imageUrl:
        "https://cdn.shopify.com/s/files/1/1136/0164/products/sanfran_grande.jpg?v=1459449289",
      address: "123 Poke Street, San Francisco, CA 94105",
      contact: "painsf@test.com",
      isFavorite: false
    }
  ];

  let editMode;

  function addMeetup(e) {
    const newMeetup = {
      id: Math.random().toString(),
      title: e.detail.title,
      subtitle: e.detail.subtitle,
      description: e.detail.description,
      imageUrl: e.detail.imageUrl,
      contact: e.detail.email,
      address: e.detail.address
    };
    meetups = [newMeetup, ...meetups];
    editMode = null;
  }

  function toggleFavorite(event) {
    const id = event.detail;
    const updatedMeetup = { ...meetups.find(m => m.id === id) };
    updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
    const meetupIndex = meetups.findIndex(m => m.id === id);
    const updatedMeetups = [...meetups];
    updatedMeetups[meetupIndex] = updatedMeetup;
    meetups = updatedMeetups;
  }

  function cancelEdit() {
    editMode = null;
  }
</script>

<style>
  #meetups {
    margin-top: 5rem;
  }

  .meetup-controls {
    margin: 1rem;
  }
</style>

<Header />

<main id="meetups">
  <div class="meetup-controls">
    <Button on:click={() => (editMode = 'add')}>New Meetup</Button>
  </div>
  {#if editMode === 'add'}
    <EditMeetup on:save={addMeetup} on:cancel={cancelEdit} />
  {/if}
  <MeetupGrid {meetups} on:togglefavorite={toggleFavorite} />
</main>
