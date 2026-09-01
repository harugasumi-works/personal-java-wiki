# Archive

<input type="text" id="archive-search" placeholder="Search articles..." style="width:100%;padding:6px;margin-bottom:10px;box-sizing:border-box;">

<table id="archive-table">
  <thead>
    <tr>
      <th onclick="sortTable(0)">Date</th>
      <th onclick="sortTable(1)">Article</th>
      <th onclick="sortTable(2)">Java Version</th>
      <th onclick="sortTable(3)">Package</th>
    </tr>
  </thead>
  <tbody id="archive-body"></tbody>
</table>

<script>
const articles = [
  { date: "2026-09-01", title: "StructuredTaskScope", slug: "structuredtaskscope", version: "25", pkg: "java.util.concurrent" },
];

function renderTable() {
  const body = document.getElementById('archive-body');
  body.innerHTML = articles.map(a => `
    <tr>
      <td>${a.date}</td>
      <td><a href="../articles/${a.slug}/">${a.title}</a></td>
      <td>${a.version}</td>
      <td>${a.pkg}</td>
    </tr>
  `).join('');
}
renderTable();

document.getElementById('archive-search').addEventListener('keyup', function () {
  var filter = this.value.toLowerCase();
  document.querySelectorAll('#archive-table tbody tr').forEach(function (row) {
    row.style.display = row.textContent.toLowerCase().includes(filter) ? '' : 'none';
  });
});

function sortTable(col) {
  var table = document.getElementById('archive-table');
  var rows = Array.from(table.tBodies[0].rows);
  var asc = table.getAttribute('data-sort-col') != col || table.getAttribute('data-sort-dir') !== 'asc';
  rows.sort(function (a, b) {
    return asc
      ? a.cells[col].textContent.trim().localeCompare(b.cells[col].textContent.trim())
      : b.cells[col].textContent.trim().localeCompare(a.cells[col].textContent.trim());
  });
  rows.forEach(function (row) { table.tBodies[0].appendChild(row); });
  table.setAttribute('data-sort-col', col);
  table.setAttribute('data-sort-dir', asc ? 'asc' : 'desc');
}
</script>