<div class="rd-dashboard">

    <p>
        There is so much more to explore. Around a quarter of the readings in Voca have at least one uncollected or unpublished work.
    </p>

    <div class="chart" id="chart-container"></div>

    <p id="reading-header">Select a reading from above or click below:</p>
    <div class="rd-table-container">
        <table class="rd-table">
            <thead>
                <tr>
                    <th>Date</th>
                    <th>Reading Title</th>
                    <th>Tracks</th>
                </tr>
            </thead>
            <tbody><!-- injected by JS --></tbody>
        </table>
    </div>

    <!-- modal dialog UI -->
    <dialog id="track-dialog">
        <div class="dlg-header">
            <h4 id="dlg-title"></h4>
            <button class="dlg-close" type="button"> ✕ </button>
        </div>
        <div id="dlg-body" style="margin-top: 1rem;"></div>
    </dialog>

</div>
<style>
  .rd-dashboard {
    color: #222;
    max-width: 100%;
  }

  .rd-filters {
    display: flex;
    gap: 1rem;
    margin-bottom: 1rem;
    align-items: center;
  }

  .rd-table-container {
    max-height: 340px;
    overflow-y: auto;
    margin-top: 1rem;
    border: 1px solid #e0e0e0;
    border-radius: 5px;
  }

  .rd-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.92rem;
    text-align: left;
  }

  .rd-table :global(thead th) {
    position: sticky;
    top: 0;
    background: rgb(215, 215, 215);
    text-align: left;
    padding: 10px;
    z-index: 1;
  }

  .rd-table :global(tbody td) {
    padding: 10px;
    border-bottom: 1px solid #eee;
    vertical-align: top;
    text-align: left;
  }

  .rd-table :global(tbody tr:hover) {
    background: #f0f7ff;
    cursor: pointer;
  }

  :global(.badge) {
    display: inline-block;
    padding: 1px 4px;
    font-size: 0.75rem;
    border-radius: 3px;
    background: #eee;
    color: #333;
  }

  :global(.badge.warn) {
    background: #fff3cd;
    color: #856404;
  }

  dialog {
    width: min(650px, 90vw);
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 1rem;
    text-align: left;
  }

  dialog::backdrop {
    background: rgba(0, 0, 0, 0.4);
  }

  .dlg-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #eee;
    padding-bottom: 0.5rem;
  }

  .dlg-close {
    background: none;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 8px;
    cursor: pointer;
  }
</style>