<script lang="ts">
  import type { CharaData } from "../types";

  let { uploaddata } = $props();

  let files: FileList | null = $state(null);
  $effect(() => {
    if (files && files.length > 0) {
      const file = files[0];
      const reader = new FileReader();

      reader.onload = (e) => {
        try {
          const content = e.target?.result as string;
          const data: CharaData[] = JSON.parse(content);
          uploaddata(data);
        } catch (error) {
          console.error("Failed to parse JSON file:", error);
        }
      };

      reader.readAsText(file);
    }
  });
</script>

<div class="row justify-content-center py-4">
  <div class="col-8">
    <div class="card">
      <div class="card-header">Instructions</div>
      <ul class="list-group list-group-flush list-group-numbered">
        <li class="list-group-item align-items-center p-3">
          Download the the Veteran List dumper
          <div class="mt-2">
            <div class="btn-group" role="group" aria-label="Links">
              <a
                type="button"
                class="btn btn-primary btn-sm"
                href="https://github.com/rockisch/umadump/releases/download/0.1/umadump.exe"
              >
                Download
              </a>
              <a
                type="button"
                class="btn btn-light btn-sm"
                href="https://github.com/rockisch/umadump"
              >
                Github
              </a>
            </div>
          </div>
        </li>
        <li class="list-group-item p-3">
          <span>Open the Veteran List page in your game</span>
          <div
            class="d-flex justify-content-center mt-2 gap-2"
            style="height: 64px;"
          >
            <img class="img-fluid" src="/guide/guide-01.png" alt="Enhance" />
            <span class="align-self-center">➜</span>
            <img class="img-fluid" src="/guide/guide-02.png" alt="Enhance" />
            <span class="align-self-center">➜</span>
            <img class="img-fluid" src="/guide/guide-03.png" alt="Enhance" />
          </div>
        </li>
        <li class="list-group-item p-3">
          <span>Run <code>umadump.exe</code></span>
        </li>
        <li class="list-group-item p-3">
          <span>Upload the generated <code>data.json</code> here</span>
          <div class="mt-2 mx-4">
            <input bind:files type="file" class="form-control" />
          </div>
        </li>
      </ul>
    </div>
  </div>
</div>
