<script>
  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import TextInput from "./UI/TextInput.svelte";
  import Button from "./UI/Button.svelte";

  let title = "";
  let subtitle = "";
  let address = "";
  let email = "";
  let description = "";
  let imageUrl = "";

  let meetups = [
    {
      id: "e1",
      title: "Paint SF",
      subtitle: "May the ART to be with you",
      description: "May the ART to be with you",
      imageUrl:
        "https://cdn.shopify.com/s/files/1/1136/0164/products/sanfran_grande.jpg?v=1459449289",
      address: "123 Poke Street, San Francisco, CA 94105",
      contact: "painsf@test.com"
    },
    {
      id: "e2",
      title: "Paint SF",
      subtitle: "May the ART to be with you",
      description: "May the ART to be with you",
      imageUrl:
        "https://cdn.shopify.com/s/files/1/1136/0164/products/sanfran_grande.jpg?v=1459449289",
      address: "123 Poke Street, San Francisco, CA 94105",
      contact: "painsf@test.com"
    }
  ];

  function addMeetup() {
    const newMeetup = {
      id: Math.random().toString(),
      title: title,
      subtitle: subtitle,
      description: description,
      imageUrl: imageUrl,
      contact: email,
      address: address
    };
    meetups = [newMeetup, ...meetups];
  }
</script>

<style>
  #meetups {
    margin-top: 5rem;
  }

  form {
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>

<Header />

<main id="meetups">
  <form on:submit|preventDefault={addMeetup}>
    <TextInput
      id="title"
      label="Title"
      type="text"
      value={title}
      on:input={event => (title = event.target.value)} />
    <TextInput
      id="subtitle"
      label="Subtitle"
      type="text"
      value={subtitle}
      on:input={event => (subtitle = event.target.value)} />
    <TextInput
      id="address"
      label="Address"
      type="text"
      value={address}
      on:input={event => (address = event.target.value)} />
    <TextInput
      id="imageUrl"
      label="Image URL"
      type="text"
      value={imageUrl}
      on:input={event => (imageUrl = event.target.value)} />
    <TextInput
      id="email"
      label="E-Mail"
      type="email"
      value={email}
      on:input={event => (email = event.target.value)} />
    <TextInput
      id="description"
      label="Description"
      controlType="textarea"
      value={description}
      on:input={event => (description = event.target.value)} />
    <Button type="submit" caption="Save" />
  </form>
  <MeetupGrid {meetups} />
</main>
