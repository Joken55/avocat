// Ajoutez ce code JavaScript à votre fichier HTML existant

// Variables pour stocker les services
let services = [
    {
        type: "Consultation",
        tarif: 150,
        forfait: "-",
        commission: 20
    },
    {
        type: "Affaire Pénale",
        tarif: 250,
        forfait: "3000€",
        commission: 25
    },
    {
        type: "Divorce",
        tarif: 200,
        forfait: "2500€",
        commission: 20
    },
    {
        type: "Commercial",
        tarif: 300,
        forfait: "5000€",
        commission: 30
    },
    {
        type: "Immobilier",
        tarif: 180,
        forfait: "1500€",
        commission: 18
    }
];

// Fonction pour afficher les services
function updateServicesTable() {
    const tbody = document.querySelector('#services table tbody');
    tbody.innerHTML = '';
    
    services.forEach((service, index) => {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td>${service.type}</td>
            <td>${service.tarif}€/h</td>
            <td>${service.forfait}</td>
            <td>${service.commission}%</td>
            <td>
                <button class="btn" onclick="modifierService(${index})">✏️ Modifier</button>
                <button class="btn btn-danger" onclick="supprimerService(${index})">🗑️ Supprimer</button>
            </td>
        `;
        tbody.appendChild(row);
    });
}

// Fonction pour modifier un service
function modifierService(index) {
    const service = services[index];
    
    // Créer un formulaire de modification
    const modal = document.createElement('div');
    modal.style.cssText = `
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0,0,0,0.5);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 1000;
    `;
    
    modal.innerHTML = `
        <div style="background: white; padding: 30px; border-radius: 15px; max-width: 500px; width: 90%;">
            <h3 style="margin-bottom: 20px; color: #2c3e50;">✏️ Modifier le Service</h3>
            <div style="margin-bottom: 15px;">
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Type de Service:</label>
                <input type="text" id="editType" value="${service.type}" style="width: 100%; padding: 10px; border: 2px solid #e9ecef; border-radius: 5px;">
            </div>
            <div style="margin-bottom: 15px;">
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Tarif Horaire (€):</label>
                <input type="number" id="editTarif" value="${service.tarif}" style="width: 100%; padding: 10px; border: 2px solid #e9ecef; border-radius: 5px;">
            </div>
            <div style="margin-bottom: 15px;">
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Forfait:</label>
                <input type="text" id="editForfait" value="${service.forfait}" style="width: 100%; padding: 10px; border: 2px solid #e9ecef; border-radius: 5px;">
            </div>
            <div style="margin-bottom: 20px;">
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Commission (%):</label>
                <input type="number" id="editCommission" value="${service.commission}" style="width: 100%; padding: 10px; border: 2px solid #e9ecef; border-radius: 5px;">
            </div>
            <div style="text-align: center;">
                <button onclick="sauvegarderService(${index})" style="background: #28a745; color: white; border: none; padding: 10px 20px; border-radius: 5px; margin-right: 10px; cursor: pointer;">💾 Sauvegarder</button>
                <button onclick="fermerModal()" style="background: #6c757d; color: white; border: none; padding: 10px 20px; border-radius: 5px; cursor: pointer;">❌ Annuler</button>
            </div>
        </div>
    `;
    
    modal.id = 'serviceModal';
    document.body.appendChild(modal);
}

// Fonction pour sauvegarder les modifications
function sauvegarderService(index) {
    const type = document.getElementById('editType').value;
    const tarif = parseInt(document.getElementById('editTarif').value);
    const forfait = document.getElementById('editForfait').value;
    const commission = parseInt(document.getElementById('editCommission').value);
    
    if (type && tarif && commission) {
        services[index] = {
            type: type,
            tarif: tarif,
            forfait: forfait,
            commission: commission
        };
        
        updateServicesTable();
        fermerModal();
        alert('Service modifié avec succès !');
    } else {
        alert('Veuillez remplir tous les champs obligatoires.');
    }
}

// Fonction pour supprimer un service
function supprimerService(index) {
    if (confirm('Êtes-vous sûr de vouloir supprimer ce service ?')) {
        services.splice(index, 1);
        updateServicesTable();
        alert('Service supprimé avec succès !');
    }
}

// Fonction pour fermer le modal
function fermerModal() {
    const modal = document.getElementById('serviceModal');
    if (modal) {
        modal.remove();
    }
}

// Fonction pour ajouter un nouveau service
function ajouterNouveauService() {
    const modal = document.createElement('div');
    modal.style.cssText = `
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0,0,0,0.5);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 1000;
    `;
    
    modal.innerHTML = `
        <div style="background: white; padding: 30px; border-radius: 15px; max-width: 500px; width: 90%;">
            <h3 style="margin-bottom: 20px; color: #2c3e50;">➕ Ajouter un Nouveau Service</h3>
            <div style="margin-bottom: 15px;">
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Type de Service:</label>
                <input type="text" id="newType" placeholder="Ex: Consultation urgente" style="width: 100%; padding: 10px; border: 2px solid #e9ecef; border-radius: 5px;">
            </div>
            <div style="margin-bottom: 15px;">
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Tarif Horaire (€):</label>
                <input type="number" id="newTarif" placeholder="150" style="width: 100%; padding: 10px; border: 2px solid #e9ecef; border-radius: 5px;">
            </div>
            <div style="margin-bottom: 15px;">
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Forfait:</label>
                <input type="text" id="newForfait" placeholder="2000€ ou -" style="width: 100%; padding: 10px; border: 2px solid #e9ecef; border-radius: 5px;">
            </div>
            <div style="margin-bottom: 20px;">
                <label style="display: block; margin-bottom: 5px; font-weight: 600;">Commission (%):</label>
                <input type="number" id="newCommission" placeholder="20" style="width: 100%; padding: 10px; border: 2px solid #e9ecef; border-radius: 5px;">
            </div>
            <div style="text-align: center;">
                <button onclick="sauvegarderNouveauService()" style="background: #28a745; color: white; border: none; padding: 10px 20px; border-radius: 5px; margin-right: 10px; cursor: pointer;">➕ Ajouter</button>
                <button onclick="fermerModal()" style="background: #6c757d; color: white; border: none; padding: 10px 20px; border-radius: 5px; cursor: pointer;">❌ Annuler</button>
            </div>
        </div>
    `;
    
    modal.id = 'serviceModal';
    document.body.appendChild(modal);
}

// Fonction pour sauvegarder un nouveau service
function sauvegarderNouveauService() {
    const type = document.getElementById('newType').value;
    const tarif = parseInt(document.getElementById('newTarif').value);
    const forfait = document.getElementById('newForfait').value || '-';
    const commission = parseInt(document.getElementById('newCommission').value);
    
    if (type && tarif && commission) {
        services.push({
            type: type,
            tarif: tarif,
            forfait: forfait,
            commission: commission
        });
        
        updateServicesTable();
        fermerModal();
        alert('Nouveau service ajouté avec succès !');
    } else {
        alert('Veuillez remplir tous les champs obligatoires.');
    }
}

// Initialiser l'affichage des services au chargement
document.addEventListener('DOMContentLoaded', function() {
    // Ajouter le bouton pour nouveau service
    const servicesSection = document.querySelector('#services .section');
    if (servicesSection) {
        const addButton = document.createElement('div');
        addButton.style.marginBottom = '20px';
        addButton.innerHTML = '<button class="btn btn-success" onclick="ajouterNouveauService()">➕ Ajouter un Service</button>';
        servicesSection.appendChild(addButton);
    }
    
    // Mettre à jour l'affichage des services
    updateServicesTable();
});
