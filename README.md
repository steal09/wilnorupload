<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wilnor's Car Shop System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .hidden {
            display: none;
        }
        /* Custom animation for toast */
        @keyframes fade-in-out {
            0% { opacity: 0; transform: translateY(-20px); }
            10% { opacity: 1; transform: translateY(0); }
            90% { opacity: 1; transform: translateY(0); }
            100% { opacity: 0; transform: translateY(-20px); }
        }
        .toast-animation {
            animation: fade-in-out 3s ease-in-out forwards;
        }
    </style>
</head>
<body class="bg-gray-100 antialiased">

    <!-- Toast Notification -->
    <div id="toast" class="hidden fixed top-5 right-5 bg-green-500 text-white py-2 px-4 rounded-lg shadow-md text-sm">
        <p id="toast-message"></p>
    </div>

    <!-- Login View -->
    <div id="login-view" class="flex items-center justify-center min-h-screen">
        <div class="w-full max-w-md p-8 space-y-6 bg-white rounded-xl shadow-lg">
            <div class="text-center">
                <h1 class="text-3xl font-bold text-gray-800">Wilnor's Car Shop</h1>
                <p class="mt-2 text-sm text-gray-600">Please sign in to access the system</p>
            </div>
            
            <form id="login-form" class="space-y-6">
                <div>
                    <label for="username" class="text-sm font-medium text-gray-700">Username</label>
                    <input id="username" name="username" type="text" required class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="wilnor">
                </div>
                <div>
                    <label for="password" class="text-sm font-medium text-gray-700">Password</label>
                    <input id="password" name="password" type="password" required class="mt-1 block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="carshop">
                </div>
                <p id="login-error" class="text-red-500 text-xs hidden">Invalid username or password.</p>
                <div>
                    <button type="submit" class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Log In
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- System View -->
    <div id="system-view" class="hidden">
        <header class="bg-white shadow-md">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center py-4">
                    <h1 class="text-2xl font-bold text-gray-800">Shop Dashboard</h1>
                    <button id="logout-button" class="text-sm font-medium text-indigo-600 hover:text-indigo-500">Logout</button>
                </div>
                <!-- Tabs -->
                <div class="border-b border-gray-200">
                    <nav class="-mb-px flex space-x-8" aria-label="Tabs">
                        <button id="tab-car-in" class="whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm border-indigo-500 text-indigo-600" aria-current="page">
                            Car In
                        </button>
                        <button id="tab-car-out" class="whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300">
                            Car Out
                        </button>
                    </nav>
                </div>
            </div>
        </header>

        <main class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
            <!-- Car In View -->
            <div id="car-in-view">
                <div class="bg-white p-8 rounded-xl shadow-lg">
                    <h2 class="text-xl font-semibold text-gray-900 mb-6">Register New Car</h2>
                    <form id="car-in-form" class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <input type="text" id="car-name" placeholder="Customer Name" required class="block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                            <input type="text" id="car-plate" placeholder="Plate Number" required class="block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                            <input type="text" id="car-model" placeholder="Car Model" required class="block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                            <input type="text" id="car-insurance" placeholder="Insurance Details" required class="block w-full px-3 py-2 bg-gray-50 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        <div>
                            <label for="car-photos" class="block text-sm font-medium text-gray-700">Photos of Damaged Area</label>
                            <input type="file" id="car-photos" multiple class="mt-1 block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-md file:border-0 file:text-sm file:font-semibold file:bg-indigo-50 file:text-indigo-600 hover:file:bg-indigo-100">
                            <p id="file-list" class="text-xs text-gray-500 mt-1"></p>
                        </div>
                        <div class="flex justify-end">
                            <button type="submit" class="inline-flex justify-center py-2 px-6 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                Save
                            </button>
                        </div>
                    </form>
                </div>
            </div>

            <!-- Car Out View -->
            <div id="car-out-view" class="hidden">
                 <div id="car-list-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Car cards will be dynamically inserted here -->
                 </div>
                 <div id="no-cars-message" class="hidden text-center py-12">
                    <svg class="mx-auto h-12 w-12 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
                        <path vector-effect="non-scaling-stroke" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 13h6m-3-3v6m-9 1V7a2 2 0 012-2h6l2 2h6a2 2 0 012 2v8a2 2 0 01-2 2H5a2 2 0 01-2-2z" />
                      </svg>
                      <h3 class="mt-2 text-sm font-medium text-gray-900">No cars in the shop</h3>
                      <p class="mt-1 text-sm text-gray-500">Get started by checking in a new car.</p>
                 </div>
            </div>
        </main>
    </div>

<script>
document.addEventListener('DOMContentLoaded', () => {

    // --- STATE MANAGEMENT ---
    // In a real application, this would be on a server or in a database.
    // For this demo, we use localStorage to persist data across reloads.
    let cars = JSON.parse(localStorage.getItem('carShopData')) || [];
    
    // --- DOM ELEMENT REFERENCES ---
    const loginView = document.getElementById('login-view');
    const systemView = document.getElementById('system-view');
    const carInView = document.getElementById('car-in-view');
    const carOutView = document.getElementById('car-out-view');
    
    const loginForm = document.getElementById('login-form');
    const loginError = document.getElementById('login-error');
    const logoutButton = document.getElementById('logout-button');
    
    const tabCarIn = document.getElementById('tab-car-in');
    const tabCarOut = document.getElementById('tab-car-out');

    const carInForm = document.getElementById('car-in-form');
    const carPhotosInput = document.getElementById('car-photos');
    const fileListDisplay = document.getElementById('file-list');

    const carListContainer = document.getElementById('car-list-container');
    const noCarsMessage = document.getElementById('no-cars-message');

    const toast = document.getElementById('toast');
    const toastMessage = document.getElementById('toast-message');


    // --- FUNCTIONS ---

    /**
     * Saves the current car list to localStorage.
     */
    const saveCarsToStorage = () => {
        localStorage.setItem('carShopData', JSON.stringify(cars));
    };

    /**
     * Shows a toast notification.
     * @param {string} message - The message to display.
     * @param {string} type - 'success' or 'error'.
     */
    const showToast = (message, type = 'success') => {
        toastMessage.textContent = message;
        toast.classList.remove('hidden', 'bg-green-500', 'bg-red-500');
        toast.classList.add(type === 'success' ? 'bg-green-500' : 'bg-red-500', 'toast-animation');
        
        // Remove the animation class after it finishes to allow re-triggering
        setTimeout(() => {
            toast.classList.add('hidden');
            toast.classList.remove('toast-animation');
        }, 3000); // Hide after 3 seconds
    };

    /**
     * Renders the list of cars in the "Car Out" tab.
     */
    const renderCarOutList = () => {
        carListContainer.innerHTML = ''; // Clear existing list
        if (cars.length === 0) {
            noCarsMessage.classList.remove('hidden');
            carListContainer.classList.add('hidden');
        } else {
            noCarsMessage.classList.add('hidden');
            carListContainer.classList.remove('hidden');
            cars.forEach((car, index) => {
                const carCard = document.createElement('div');
                carCard.className = 'bg-white rounded-xl shadow-lg overflow-hidden transform hover:scale-105 transition-transform duration-300';
                carCard.innerHTML = `
                    <div class="p-6">
                        <div class="flex justify-between items-start">
                             <h3 class="text-lg font-bold text-gray-800">${car.plate}</h3>
                             <span class="px-2 py-1 text-xs font-semibold leading-5 text-green-800 bg-green-100 rounded-full">${car.model}</span>
                        </div>
                        <p class="mt-2 text-sm text-gray-600"><strong>Customer:</strong> ${car.name}</p>
                        <p class="mt-1 text-sm text-gray-600"><strong>Insurance:</strong> ${car.insurance}</p>
                        <p class="mt-1 text-sm text-gray-500"><strong>Files:</strong> ${car.photos.join(', ')}</p>
                        <div class="mt-4 pt-4 border-t border-gray-200">
                            <button data-index="${index}" class="car-out-button w-full text-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500">
                                Check Out
                            </button>
                        </div>
                    </div>
                `;
                carListContainer.appendChild(carCard);
            });
        }
    };

    /**
     * Switches between the 'Car In' and 'Car Out' tabs.
     * @param {string} targetTab - 'in' or 'out'.
     */
    const switchTab = (targetTab) => {
        if (targetTab === 'in') {
            // UI update for tabs
            tabCarIn.classList.add('border-indigo-500', 'text-indigo-600');
            tabCarIn.classList.remove('border-transparent', 'text-gray-500', 'hover:text-gray-700', 'hover:border-gray-300');
            tabCarOut.classList.add('border-transparent', 'text-gray-500', 'hover:text-gray-700', 'hover:border-gray-300');
            tabCarOut.classList.remove('border-indigo-500', 'text-indigo-600');
            
            // Show/Hide views
            carInView.classList.remove('hidden');
            carOutView.classList.add('hidden');
        } else { // targetTab === 'out'
             // UI update for tabs
            tabCarOut.classList.add('border-indigo-500', 'text-indigo-600');
            tabCarOut.classList.remove('border-transparent', 'text-gray-500', 'hover:text-gray-700', 'hover:border-gray-300');
            tabCarIn.classList.add('border-transparent', 'text-gray-500', 'hover:text-gray-700', 'hover:border-gray-300');
            tabCarIn.classList.remove('border-indigo-500', 'text-indigo-600');
            
            // Show/Hide views
            carOutView.classList.remove('hidden');
            carInView.classList.add('hidden');

            renderCarOutList();
        }
    };
    

    // --- EVENT LISTENERS ---

    // Handle Login
    loginForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const username = e.target.username.value;
        const password = e.target.password.value;

        if (username.toLowerCase() === 'wilnor' && password.toLowerCase() === 'carshop') {
            loginView.classList.add('hidden');
            systemView.classList.remove('hidden');
            loginError.classList.add('hidden');
            sessionStorage.setItem('isLoggedIn', 'true'); // Keep user logged in for the session
        } else {
            loginError.classList.remove('hidden');
        }
    });

    // Handle Logout
    logoutButton.addEventListener('click', () => {
        systemView.classList.add('hidden');
        loginView.classList.remove('hidden');
        loginForm.reset();
        sessionStorage.removeItem('isLoggedIn'); // Log the user out
    });

    // Handle Tab Switching
    tabCarIn.addEventListener('click', () => switchTab('in'));
    tabCarOut.addEventListener('click', () => switchTab('out'));

    // Handle "Car In" Form Submission
    carInForm.addEventListener('submit', (e) => {
        e.preventDefault();
        
        const photoFiles = carPhotosInput.files;
        const photoNames = photoFiles.length > 0 ? Array.from(photoFiles).map(file => file.name) : ['No photos'];

        const newCar = {
            name: document.getElementById('car-name').value,
            plate: document.getElementById('car-plate').value,
            model: document.getElementById('car-model').value,
            insurance: document.getElementById('car-insurance').value,
            photos: photoNames,
        };

        cars.push(newCar);
        saveCarsToStorage();
        showToast('Car successfully saved!');
        carInForm.reset();
        fileListDisplay.textContent = '';
    });
    
    // Display names of selected files
    carPhotosInput.addEventListener('change', (e) => {
        const files = e.target.files;
        if (files.length > 0) {
            fileListDisplay.textContent = `${files.length} file(s) selected.`;
        } else {
            fileListDisplay.textContent = '';
        }
    });

    // Handle "Car Out" button clicks using event delegation
    carListContainer.addEventListener('click', (e) => {
        if (e.target && e.target.classList.contains('car-out-button')) {
            const carIndex = parseInt(e.target.dataset.index, 10);
            
            // Remove car from array
            cars.splice(carIndex, 1);
            
            // Update storage and re-render the list
            saveCarsToStorage();
            renderCarOutList();
            showToast('Car checked out.', 'success');
        }
    });

    // --- INITIALIZATION ---
    // Check if user is already logged in (e.g., after a page refresh)
    if (sessionStorage.getItem('isLoggedIn') === 'true') {
        loginView.classList.add('hidden');
        systemView.classList.remove('hidden');
        switchTab('in'); // Default to 'Car In' tab
    }
});
</script>

</body>
</html>

