<script>

/**
 * 

DONE:

* basic upload form
* colected data into an object

TODO

* write json file to public filesystem
* change over from existing stores to new ones
* adjust upload logic to accept small videos and pdf failes as well?

*/


import { galleryStore } from '$routes/upload-test/stores'
import { get } from 'svelte/store';

function getFormData() {
  // console.log("clicked")
  let _form = document.querySelector('#form-media-upload')
  console.log(_form)

  let title = _form[0].value
  let desc = _form[1].value
  // console.log('textarea', _form[1])
  let media = get(galleryStore).publicImages

  let result = {
    title: title,
    description: desc,
    media: media
  }
  console.log(result)

  document.querySelector('#txt-debug-textarea').textContent = JSON.stringify(result, null, '  ')

}

</script>

<div style="text-align: left; padding: 20px;">
  <form action="#" name="media-upload" id="form-media-upload">

    <div>
      <label class="label" for="work-title">
        Title
      </label>
      <input type="text" placeholder="Create a title" class="input w-full input-bordered" name="work-title"/>
    </div>

    <div>
      <label for="work-description" class="label">
        Description
      </label>
      <textarea 
        class="textarea textarea-bordered w-full"
        name="work-description" 
        id="form-work-description" 
        cols="30" 
        rows="10"></textarea>
    </div>
    

    <h3 style="margin-top: 20px">Drop files here to upload</h3>
      <slot/>
    <div>
      <button on:click={getFormData} class="btn-primary btn-wide">Save</button>
    </div>
  </form>
</div>

<div>
  <h2>DEBUG</h2>

  <textarea name="debug-textarea" id="txt-debug-textarea" class="textarea textarea-bordered w-full"></textarea>
</div>