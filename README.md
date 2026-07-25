<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>Suivi Clients dōTERRA</title>
<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  -webkit-user-select: none;
  user-select: none;
}

html, body {
  width: 100%;
  height: 100%;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background: #f5f5f3;
  color: #1a1a1a;
  -webkit-touch-callout: none;
}

body {
  padding: 10px;
  padding-bottom: 20px;
  overflow-y: auto;
  -webkit-user-select: text;
  user-select: text;
}

.app {
  max-width: 950px;
  margin: 0 auto;
}

/* TOPBAR */
.topbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: linear-gradient(135deg, #2d6a4f 0%, #1d3a34 100%);
  border-radius: 12px;
  padding: 14px;
  margin-bottom: 14px;
  box-shadow: 0 2px 8px rgba(45, 106, 79, 0.2);
  gap: 10px;
}

.topbar h1 {
  font-size: 18px;
  color: #fff;
  font-weight: 600;
  letter-spacing: 0.5px;
  flex: 1;
}

.topbar-right {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
  justify-content: flex-end;
}

/* BOUTONS */
.btn {
  padding: 10px 14px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 13px;
  font-weight: 500;
  transition: all 0.2s ease;
  white-space: nowrap;
  -webkit-appearance: none;
  appearance: none;
  text-decoration: none;
  display: inline-block;
}

.btn-primary {
  background: #52b788;
  color: white;
}

.btn-primary:active {
  background: #40916c;
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.2);
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.4);
}

.btn-secondary:active {
  background: rgba(255, 255, 255, 0.3);
}

.btn-danger {
  background: #d62828;
  color: white;
}

.btn-danger:active {
  background: #a71c1c;
}

.btn-small {
  padding: 8px 12px;
  font-size: 12px;
}

/* MODAL */
.modal {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  z-index: 2000;
  align-items: center;
  justify-content: center;
  padding: 10px;
}

.modal.open {
  display: flex;
}

.modal-content {
  background: white;
  border-radius: 16px;
  padding: 20px;
  max-width: 500px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
  animation: slideUp 0.3s ease;
}

@keyframes slideUp {
  from {
    transform: translateY(30px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
  border-bottom: 2px solid #f0f0f0;
  padding-bottom: 12px;
}

.modal-header h2 {
  font-size: 20px;
  color: #2d6a4f;
}

.close-btn {
  background: none;
  border: none;
  font-size: 28px;
  cursor: pointer;
  color: #999;
  padding: 0;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.close-btn:active {
  color: #333;
}

/* FORMULAIRE */
.form-group {
  margin-bottom: 14px;
}

.form-group label {
  display: block;
  font-weight: 600;
  color: #2d6a4f;
  margin-bottom: 6px;
  font-size: 13px;
}

.form-group input,
.form-group textarea,
.form-group select {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-family: inherit;
  font-size: 14px;
  -webkit-appearance: none;
  appearance: none;
  background: white;
}

.form-group input:focus,
.form-group textarea:focus,
.form-group select:focus {
  outline: none;
  border-color: #52b788;
  box-shadow: 0 0 0 3px rgba(82, 183, 136, 0.1);
}

.form-group textarea {
  resize: vertical;
  min-height: 80px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

/* LISTE */
.clients-list {
  display: grid;
  gap: 12px;
}

.client-card {
  background: white;
  border-radius: 12px;
  padding: 14px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: all 0.2s ease;
  border-left: 4px solid #52b788;
}

.client-card:active {
  box-shadow: 0 4px 12px rgba(45, 106, 79, 0.2);
  transform: translateY(-2px);
}

.client-card.pinned {
  border-left-color: #ffc107;
  background: #fffbf0;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: start;
  margin-bottom: 8px;
}

.card-title {
  font-weight: 700;
  font-size: 16px;
  color: #2d6a4f;
}

.card-date {
  font-size: 12px;
  color: #999;
}

.card-info {
  font-size: 13px;
  color: #555;
  margin: 4px 0;
}

.pin-btn {
  background: none;
  border: none;
  font-size: 18px;
  cursor: pointer;
  padding: 4px 8px;
}

/* ONGLETS */
.tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 14px;
  border-bottom: 1px solid #ddd;
  overflow-x: auto;
}

.tab-btn {
  padding: 10px 14px;
  border: none;
  background: none;
  color: #999;
  cursor: pointer;
  font-weight: 500;
  border-bottom: 3px solid transparent;
  font-size: 13px;
  white-space: nowrap;
}

.tab-btn.active {
  color: #2d6a4f;
  border-bottom-color: #52b788;
}

.tab-content {
  display: none;
}

.tab-content.active {
  display: block;
}

/* NOTICE */
.notice-section {
  margin-bottom: 20px;
}

.notice-section h3 {
  color: #2d6a4f;
  font-size: 16px;
  margin-bottom: 8px;
  margin-top: 14px;
}

.notice-section:first-child h3 {
  margin-top: 0;
}

.notice-section p,
.notice-section li {
  font-size: 13px;
  line-height: 1.6;
  color: #555;
  margin-bottom: 6px;
}

.notice-section ul {
  margin-left: 16px;
}

.notice-section strong {
  color: #2d6a4f;
}

/* EMPTY STATE */
.empty-state {
  text-align: center;
  padding: 40px 20px;
  color: #999;
}

.empty-state-icon {
  font-size: 48px;
  margin-bottom: 12px;
}

.empty-state p {
  font-size: 14px;
  margin-bottom: 16px;
}

/* SEARCH */
.search-box {
  margin-bottom: 14px;
}

.search-box input {
  width: 100%;
  padding: 10px 14px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 14px;
}

/* RESPONSIVE */
@media (max-width: 600px) {
  body {
    padding: 8px;
  }

  .topbar {
    padding: 10px;
    margin-bottom: 10px;
  }

  .topbar h1 {
    font-size: 16px;
  }

  .btn {
    padding: 8px 12px;
    font-size: 12px;
  }

  .modal-content {
    padding: 16px;
    border-radius: 12px;
  }

  .client-card {
    padding: 12px;
  }
}

/* LOADING */
.loading {
  opacity: 0.6;
  pointer-events: none;
}

</style>
</head>
<body>

<div class="app">
  <!-- TOPBAR -->
  <div class="topbar">
    <h1>🌿 dōTERRA Clients</h1>
    <div class="topbar-right">
      <button class="btn btn-primary btn-small" onclick="openNewClientModal()">➕ Nouveau client</button>
      <button class="btn btn-secondary btn-small" onclick="openNoticeModal()">📖 Notice</button>
      <button class="btn btn-secondary btn-small" onclick="exportData()">⬇️ Export</button>
      <button class="btn btn-secondary btn-small" onclick="document.getElementById('importFile').click()">⬆️ Import</button>
      <input type="file" id="importFile" style="display:none" accept=".json" onchange="handleImport(event)">
    </div>
  </div>

  <!-- SEARCH -->
  <div class="search-box">
    <input type="text" id="searchInput" placeholder="🔍 Rechercher un client..." onkeyup="filterClients()">
  </div>

  <!-- MODALS -->
  
  <!-- MODAL: NOUVEAU CLIENT -->
  <div id="newClientModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2>➕ Nouveau Client</h2>
        <button class="close-btn" onclick="closeNewClientModal()">✕</button>
      </div>
      <form onsubmit="addClient(event)">
        <div class="form-group">
          <label>Nom du client *</label>
          <input type="text" id="clientName" required>
        </div>
        <div class="form-group">
          <label>Email</label>
          <input type="email" id="clientEmail">
        </div>
        <div class="form-group">
          <label>Téléphone</label>
          <input type="tel" id="clientPhone">
        </div>
        <div class="form-group">
          <label>Date de naissance</label>
          <input type="date" id="clientBirthday">
        </div>
        <div class="form-group">
          <label>Numéro de client (si applicable)</label>
          <input type="text" id="clientNumber">
        </div>
        <div class="form-group">
          <label>Produits achetés</label>
          <textarea id="clientProducts" placeholder="Listez les produits..."></textarea>
        </div>
        <div class="form-group">
          <label>Notes permanentes</label>
          <textarea id="clientPermanentNotes" placeholder="Notes qui resteront toujours visibles..."></textarea>
        </div>
        <button type="submit" class="btn btn-primary" style="width: 100%; margin-top: 12px;">✅ Ajouter le client</button>
      </form>
    </div>
  </div>

  <!-- MODAL: DÉTAILS CLIENT -->
  <div id="clientDetailModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 id="detailTitle">Détails Client</h2>
        <button class="close-btn" onclick="closeDetailModal()">✕</button>
      </div>
      <div id="detailContent"></div>
    </div>
  </div>

  <!-- MODAL: NOTICE -->
  <div id="noticeModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2>📖 Guide d'Utilisation</h2>
        <button class="close-btn" onclick="closeNoticeModal()">✕</button>
      </div>
      <div id="noticeContent"></div>
    </div>
  </div>

  <!-- LISTE CLIENTS -->
  <div id="clientsList" class="clients-list"></div>

</div>

<script>

// DONNÉES
let clients = JSON.parse(localStorage.getItem('doterra_clients')) || [];
let currentClientId = null;

const NOTICE_HTML = `
<div class="notice-section">
  <h3>🎯 Vue d'ensemble</h3>
  <p>Cette application vous permet de suivre vos clients dōTERRA facilement depuis <strong>n'importe quel appareil</strong> (téléphone, tablette, ordinateur).</p>
</div>

<div class="notice-section">
  <h3>➕ Ajouter un nouveau client</h3>
  <p>Cliquez sur le bouton <strong>"➕ Nouveau client"</strong> en haut.</p>
  <p>Remplissez les informations:</p>
  <ul>
    <li><strong>Nom du client</strong> (obligatoire)</li>
    <li><strong>Email</strong></li>
    <li><strong>Téléphone</strong></li>
    <li><strong>Date de naissance</strong></li>
    <li><strong>Numéro de client</strong> (si vous l'avez reçu de dōTERRA)</li>
    <li><strong>Produits achetés</strong> (vous pourrez modifier plus tard)</li>
    <li><strong>Notes permanentes</strong> (restera visible en permanence)</li>
  </ul>
</div>

<div class="notice-section">
  <h3>👁️ Consulter un client</h3>
  <p>Cliquez sur la carte d'un client pour voir tous ses détails et son historique.</p>
</div>

<div class="notice-section">
  <h3>📌 Épingler un client</h3>
  <p>Cliquez sur l'icône <strong>⭐</strong> pour épingler un client en priorité. Les clients épinglés apparaissent en premier avec un fond jaune.</p>
</div>

<div class="notice-section">
  <h3>📞 Ajouter une entrevue</h3>
  <p>Dans la page d'un client, cliquez sur <strong>"+ Ajouter entrevue"</strong> pour enregistrer une rencontre avec:</p>
  <ul>
    <li><strong>Date de l'entrevue</strong></li>
    <li><strong>Notes</strong> (ce que vous avez discuté)</li>
    <li><strong>À faire</strong> (actions à prendre)</li>
    <li><strong>Rappel</strong> (points importants)</li>
    <li><strong>Idées</strong> (produits à suggérer, etc.)</li>
  </ul>
</div>

<div class="notice-section">
  <h3>🔍 Rechercher</h3>
  <p>Utilisez la barre de recherche en haut pour trouver rapidement un client par son nom.</p>
</div>

<div class="notice-section">
  <h3>⬇️ Exporter / ⬆️ Importer</h3>
  <p><strong>Exporter:</strong> Sauvegardez vos données en JSON (format texte sécurisé).</p>
  <p><strong>Importer:</strong> Restaurez vos données depuis un fichier JSON.</p>
</div>

<div class="notice-section">
  <h3>💾 Sauvegarde</h3>
  <p>Vos données sont automatiquement sauvegardées sur votre appareil. Enregistrez ce fichier HTML dans Dropbox pour l'utiliser partout!</p>
</div>

<div class="notice-section">
  <h3>⚠️ Attention sur iPhone</h3>
  <p>Assurez-vous que le fichier HTML se termine par <strong>.html</strong> et ouvrez-le toujours depuis le même navigateur pour garder vos données.</p>
</div>
`;

// RENDER
function render() {
  const list = document.getElementById('clientsList');
  
  if (clients.length === 0) {
    list.innerHTML = `
      <div class="empty-state">
        <div class="empty-state-icon">📋</div>
        <p>Aucun client pour le moment</p>
        <p style="font-size: 12px; color: #ccc;">Cliquez sur "➕ Nouveau client" pour commencer</p>
      </div>
    `;
    return;
  }

  const sortedClients = [...clients].sort((a, b) => {
    if (a.pinned === b.pinned) return 0;
    return a.pinned ? -1 : 1;
  });

  list.innerHTML = sortedClients.map(client => `
    <div class="client-card ${client.pinned ? 'pinned' : ''}" onclick="openClientDetail('${client.id}')">
      <div class="card-header">
        <div>
          <div class="card-title">${escapeHtml(client.name)}</div>
          <div class="card-date">${client.firstOrderDate ? '📅 ' + formatDate(client.firstOrderDate) : 'Pas de date'}</div>
        </div>
        <button class="pin-btn" onclick="togglePin('${client.id}', event)">
          ${client.pinned ? '⭐' : '☆'}
        </button>
      </div>
      <div class="card-info">📞 ${client.phone || '—'}</div>
      <div class="card-info">📧 ${client.email || '—'}</div>
      <div class="card-info">🆔 ${client.number || '—'}</div>
    </div>
  `).join('');
}

// FILTER
function filterClients() {
  const search = document.getElementById('searchInput').value.toLowerCase();
  const cards = document.querySelectorAll('.client-card');
  
  cards.forEach(card => {
    const text = card.textContent.toLowerCase();
    card.style.display = text.includes(search) ? '' : 'none';
  });
}

// OPEN NEW CLIENT MODAL
function openNewClientModal() {
  document.getElementById('newClientModal').classList.add('open');
}

function closeNewClientModal() {
  document.getElementById('newClientModal').classList.remove('open');
  document.getElementById('newClientModal').querySelectorAll('input, textarea').forEach(el => el.value = '');
}

// ADD CLIENT
function addClient(e) {
  e.preventDefault();
  
  const client = {
    id: Date.now().toString(),
    name: document.getElementById('clientName').value.trim(),
    email: document.getElementById('clientEmail').value.trim(),
    phone: document.getElementById('clientPhone').value.trim(),
    birthday: document.getElementById('clientBirthday').value,
    number: document.getElementById('clientNumber').value.trim(),
    products: document.getElementById('clientProducts').value.trim(),
    permanentNotes: document.getElementById('clientPermanentNotes').value.trim(),
    firstOrderDate: new Date().toISOString().split('T')[0],
    pinned: false,
    interviews: []
  };

  clients.push(client);
  saveToStorage();
  closeNewClientModal();
  render();
  document.getElementById('searchInput').value = '';
}

// OPEN CLIENT DETAIL
function openClientDetail(id) {
  currentClientId = id;
  const client = clients.find(c => c.id === id);
  if (!client) return;

  const detailContent = document.getElementById('detailContent');
  
  detailContent.innerHTML = `
    <div class="tabs">
      <button class="tab-btn active" onclick="switchTab('infoTab', event)">ℹ️ Infos</button>
      <button class="tab-btn" onclick="switchTab('interviewsTab', event)">📞 Entrevues</button>
    </div>

    <div id="infoTab" class="tab-content active">
      <div class="form-group">
        <label><strong>Nom</strong></label>
        <input type="text" value="${escapeHtml(client.name)}" onchange="updateClient('name', this.value)">
      </div>
      <div class="form-group">
        <label><strong>Email</strong></label>
        <input type="email" value="${escapeHtml(client.email)}" onchange="updateClient('email', this.value)">
      </div>
      <div class="form-group">
        <label><strong>Téléphone</strong></label>
        <input type="tel" value="${escapeHtml(client.phone)}" onchange="updateClient('phone', this.value)">
      </div>
      <div class="form-group">
        <label><strong>Date de naissance</strong></label>
        <input type="date" value="${client.birthday}" onchange="updateClient('birthday', this.value)">
      </div>
      <div class="form-group">
        <label><strong>Numéro de client</strong></label>
        <input type="text" value="${escapeHtml(client.number)}" onchange="updateClient('number', this.value)">
      </div>
      <div class="form-group">
        <label><strong>Produits achetés</strong></label>
        <textarea onchange="updateClient('products', this.value)">${escapeHtml(client.products)}</textarea>
      </div>
      <div class="form-group">
        <label><strong>Notes permanentes</strong></label>
        <textarea onchange="updateClient('permanentNotes', this.value)">${escapeHtml(client.permanentNotes)}</textarea>
      </div>
      <div class="form-group">
        <label><strong>Date de 1ère commande</strong></label>
        <input type="date" value="${client.firstOrderDate}" onchange="updateClient('firstOrderDate', this.value)">
      </div>
      <button class="btn btn-danger" style="width: 100%; margin-top: 16px;" onclick="deleteClient('${id}')">🗑️ Supprimer ce client</button>
    </div>

    <div id="interviewsTab" class="tab-content">
      <button class="btn btn-primary" style="width: 100%; margin-bottom: 14px;" onclick="openAddInterviewModal('${id}')">➕ Ajouter entrevue</button>
      <div id="interviewsList"></div>
    </div>
  `;

  renderInterviews(id);
  
  document.getElementById('detailTitle').textContent = escapeHtml(client.name);
  document.getElementById('clientDetailModal').classList.add('open');
}

function closeDetailModal() {
  document.getElementById('clientDetailModal').classList.remove('open');
  currentClientId = null;
}

// INTERVIEWS
function renderInterviews(clientId) {
  const client = clients.find(c => c.id === clientId);
  if (!client) return;

  const list = document.getElementById('interviewsList');
  
  if (client.interviews.length === 0) {
    list.innerHTML = '<p style="text-align: center; color: #999; font-size: 13px;">Aucune entrevue</p>';
    return;
  }

  list.innerHTML = client.interviews.map((interview, idx) => `
    <div style="background: #f9f9f9; border-radius: 8px; padding: 12px; margin-bottom: 10px; border-left: 3px solid #52b788;">
      <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 8px;">
        <strong style="color: #2d6a4f;">📅 ${formatDate(interview.date)}</strong>
        <button class="btn btn-small btn-danger" onclick="deleteInterview('${clientId}', ${idx})">🗑️</button>
      </div>
      ${interview.notes ? `<p style="font-size: 12px; color: #333; margin-bottom: 6px;"><strong>📝 Notes:</strong> ${escapeHtml(interview.notes)}</p>` : ''}
      ${interview.todo ? `<p style="font-size: 12px; color: #d62828; margin-bottom: 6px;"><strong>✓ À faire:</strong> ${escapeHtml(interview.todo)}</p>` : ''}
      ${interview.reminder ? `<p style="font-size: 12px; color: #ff6b6b; margin-bottom: 6px;"><strong>‼️ Rappel:</strong> ${escapeHtml(interview.reminder)}</p>` : ''}
      ${interview.idea ? `<p style="font-size: 12px; color: #40916c; margin-bottom: 0;"><strong>💡 Idée:</strong> ${escapeHtml(interview.idea)}</p>` : ''}
    </div>
  `).join('');
}

// ADD INTERVIEW MODAL
function openAddInterviewModal(clientId) {
  const modal = document.createElement('div');
  modal.className = 'modal open';
  modal.id = 'interviewModal';
  modal.innerHTML = `
    <div class="modal-content">
      <div class="modal-header">
        <h2>➕ Nouvelle entrevue</h2>
        <button class="close-btn" onclick="document.getElementById('interviewModal').remove()">✕</button>
      </div>
      <form onsubmit="addInterview(event, '${clientId}')">
        <div class="form-group">
          <label>Date de l'entrevue *</label>
          <input type="date" id="interviewDate" required>
        </div>
        <div class="form-group">
          <label>📝 Notes</label>
          <textarea id="interviewNotes" placeholder="Ce qui a été discuté..."></textarea>
        </div>
        <div class="form-group">
          <label>✓ À faire</label>
          <textarea id="interviewTodo" placeholder="Actions à prendre..."></textarea>
        </div>
        <div class="form-group">
          <label>‼️ Rappel</label>
          <textarea id="interviewReminder" placeholder="Points importants à retenir..."></textarea>
        </div>
        <div class="form-group">
          <label>💡 Idée</label>
          <textarea id="interviewIdea" placeholder="Produits à suggérer, idées..."></textarea>
        </div>
        <button type="submit" class="btn btn-primary" style="width: 100%; margin-top: 12px;">✅ Ajouter entrevue</button>
      </form>
    </div>
  `;
  document.body.appendChild(modal);
  modal.querySelector('#interviewDate').valueAsDate = new Date();
}

function addInterview(e, clientId) {
  e.preventDefault();
  
  const client = clients.find(c => c.id === clientId);
  if (!client) return;

  const interview = {
    date: document.getElementById('interviewDate').value,
    notes: document.getElementById('interviewNotes').value.trim(),
    todo: document.getElementById('interviewTodo').value.trim(),
    reminder: document.getElementById('interviewReminder').value.trim(),
    idea: document.getElementById('interviewIdea').value.trim()
  };

  client.interviews.push(interview);
  saveToStorage();
  document.getElementById('interviewModal').remove();
  renderInterviews(clientId);
}

function deleteInterview(clientId, idx) {
  const client = clients.find(c => c.id === clientId);
  if (client && confirm('Confirmer la suppression?')) {
    client.interviews.splice(idx, 1);
    saveToStorage();
    renderInterviews(clientId);
  }
}

// UTILITIES
function updateClient(field, value) {
  const client = clients.find(c => c.id === currentClientId);
  if (client) {
    client[field] = value;
    saveToStorage();
  }
}

function togglePin(id, e) {
  e.stopPropagation();
  const client = clients.find(c => c.id === id);
  if (client) {
    client.pinned = !client.pinned;
    saveToStorage();
    render();
  }
}

function deleteClient(id) {
  if (confirm('Êtes-vous sûr? Cette action ne peut pas être annulée.')) {
    clients = clients.filter(c => c.id !== id);
    saveToStorage();
    closeDetailModal();
    render();
  }
}

function switchTab(tabId, e) {
  const tabs = e.target.parentElement.querySelectorAll('.tab-btn');
  const contents = document.querySelectorAll('.tab-content');
  
  tabs.forEach(t => t.classList.remove('active'));
  contents.forEach(c => c.classList.remove('active'));
  
  e.target.classList.add('active');
  document.getElementById(tabId).classList.add('active');
}

function openNoticeModal() {
  document.getElementById('noticeContent').innerHTML = NOTICE_HTML;
  document.getElementById('noticeModal').classList.add('open');
}

function closeNoticeModal() {
  document.getElementById('noticeModal').classList.remove('open');
}

function exportData() {
  const dataStr = JSON.stringify(clients, null, 2);
  const dataBlob = new Blob([dataStr], { type: 'application/json' });
  const url = URL.createObjectURL(dataBlob);
  const link = document.createElement('a');
  link.href = url;
  link.download = `doterra_clients_${new Date().toISOString().split('T')[0]}.json`;
  link.click();
  URL.revokeObjectURL(url);
}

function importData() {
  document.getElementById('importFile').click();
}

function handleImport(e) {
  const file = e.target.files[0];
  if (!file) return;
  
  const reader = new FileReader();
  reader.onload = function(event) {
    try {
      const imported = JSON.parse(event.target.result);
      if (Array.isArray(imported)) {
        clients = imported;
        saveToStorage();
        render();
        alert('✅ Données importées avec succès!');
      } else {
        alert('❌ Format invalide.');
      }
    } catch (err) {
      alert('❌ Erreur lors de l\'import.');
    }
  };
  reader.readAsText(file);
  e.target.value = '';
}

function saveToStorage() {
  localStorage.setItem('doterra_clients', JSON.stringify(clients));
}

function formatDate(dateStr) {
  const date = new Date(dateStr + 'T00:00:00');
  return date.toLocaleDateString('fr-FR', { day: 'numeric', month: 'long', year: 'numeric' });
}

function escapeHtml(text) {
  const div = document.createElement('div');
  div.textContent = text;
  return div.innerHTML;
}

// INIT
document.addEventListener('DOMContentLoaded', function() {
  render();
  
  // Éviter le zoom sur double-tap iOS
  document.addEventListener('touchend', function() {}, false);
});

</script>

</body>
</html># doterra_suivi-clients
