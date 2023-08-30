<script lang="ts">
  import { onDestroy } from 'svelte'
  import { goto } from '$app/navigation'

  import { sessionStore } from '$src/stores'
  import { AREAS, galleryStore } from '$routes/upload-test/stores'
  import Dropzone from '$routes/upload-test/components/upload/Dropzone.svelte'
  import ImageGallery from '$routes/upload-test/components/imageGallery/ImageGallery.svelte'
  import MediaUpload from './components/upload/MediaUpload.svelte'

  /**
   * Tab between the public/private areas and load associated images
   * @param area
   */
  const handleChangeTab: (area: AREAS) => void = area =>
    galleryStore.update(store => ({
      ...store,
      selectedArea: area
    }))

  // If the user is not authed redirect them to the home page
  const unsubscribe = sessionStore.subscribe(newState => {
    if (!newState.loading && !newState.session) {
      goto('/')
    }
  })

  onDestroy(unsubscribe)
</script>

<div class="p-2 mb-14 text-center">
  {#if $sessionStore.session}
    <div class="flex items-center justify-center translate-y-1/2 w-fit m-auto">
      <div class="tabs border-2 overflow-hidden border-base-content rounded-lg">
          <button
            on:click={() => { console.log('click') }}
            class="tab h-10 font-bold text-sm ease-in tab-active bg-base-content text-base-100"
          >
            Uploaded Media
          </button>
      </div>
    </div>

    <Dropzone>
      <MediaUpload>
        <ImageGallery />
      </MediaUpload>
      
    </Dropzone>
    
  {/if}
</div>
