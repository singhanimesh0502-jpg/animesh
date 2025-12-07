# animesh
this is my first repositary
<br>
author - animesh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BOOKStore - Your Study Partner</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', sans-serif;
        }
        
        .book-card {
            transition: all 0.3s ease;
        }
        
        .book-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        
        .book-card img {
            transition: transform 0.3s ease;
        }
        
        .book-card:hover img {
            transform: scale(1.05);
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 9999;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }
        
        .modal.active {
            display: flex;
        }
        
        .loading {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 9999;
            align-items: center;
            justify-content: center;
        }
        
        .loading.active {
            display: flex;
        }
        
        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #2563eb;
            border-radius: 50%;
            width: 64px;
            height: 64px;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        
        ::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 4px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
    </style>
</head>
<body class="min-h-screen bg-gradient-to-br from-blue-50 via-white to-purple-50">
    
    <!-- Header -->
    <header class="bg-white shadow-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 py-4">
            <div class="flex items-center justify-between mb-4">
                <div class="flex items-center gap-3">
                    <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"></path>
                    </svg>
                    <h1 class="text-2xl font-bold bg-gradient-to-r from-blue-600 to-purple-600 bg-clip-text text-transparent">
                        BOOKStore
                    </h1>
                </div>
                <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
                    Login
                </button>
            </div>

            <!-- Search Bar -->
            <div class="relative">
                <svg class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                </svg>
                <input
                    type="text"
                    id="searchInput"
                    placeholder="Search books, authors, subjects..."
                    class="w-full pl-12 pr-4 py-3 border-2 border-gray-200 rounded-xl focus:border-blue-500 focus:outline-none transition-colors"
                    oninput="filterBooks()"
                />
            </div>
        </div>
    </header>

    <div class="max-w-7xl mx-auto px-4 py-8">
        
        <!-- Hero Section -->
        <div class="bg-gradient-to-r from-blue-600 to-purple-600 rounded-2xl p-8 mb-8 text-white relative overflow-hidden">
            <div class="relative z-10">
                <h2 class="text-4xl font-bold mb-3">Your Study Partner 📚</h2>
                <p class="text-lg opacity-90 mb-6">Access thousands of free books, PDFs, and study materials</p>
                <div class="flex gap-4 flex-wrap">
                    <div class="bg-white/20 backdrop-blur-sm rounded-lg px-4 py-2">
                        <div class="text-2xl font-bold">15K+</div>
                        <div class="text-sm opacity-90">Books</div>
                    </div>
                    <div class="bg-white/20 backdrop-blur-sm rounded-lg px-4 py-2">
                        <div class="text-2xl font-bold">50K+</div>
                        <div class="text-sm opacity-90">Downloads</div>
                    </div>
                    <div class="bg-white/20 backdrop-blur-sm rounded-lg px-4 py-2">
                        <div class="text-2xl font-bold">100%</div>
                        <div class="text-sm opacity-90">Free</div>
                    </div>
                </div>
            </div>
            <div class="absolute right-0 top-0 w-64 h-64 bg-white/10 rounded-full -mr-32 -mt-32"></div>
            <div class="absolute right-20 bottom-0 w-48 h-48 bg-white/10 rounded-full -mb-24"></div>
        </div>

        <!-- Filters -->
        <div class="bg-white rounded-xl shadow-md p-4 mb-6">
            <div class="flex items-center justify-between mb-4">
                <h3 class="font-semibold text-gray-700 flex items-center gap-2">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z"></path>
                    </svg>
                    Filters
                </h3>
                <button onclick="toggleFilters()" class="md:hidden text-blue-600 flex items-center gap-1">
                    <span id="filterToggleText">Show</span>
                    <svg id="filterChevron" class="w-4 h-4 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                    </svg>
                </button>
            </div>
            
            <div id="filterSection" class="hidden md:flex flex-wrap gap-4">
                <div class="flex-1 min-w-[200px]">
                    <label class="block text-sm font-medium text-gray-600 mb-2">Class</label>
                    <select id="classFilter" onchange="filterBooks()" class="w-full px-4 py-2 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none">
                        <option value="all">All Classes</option>
                        <option value="X">Class X</option>
                        <option value="XII">Class XII</option>
                    </select>
                </div>

                <div class="flex-1 min-w-[200px]">
                    <label class="block text-sm font-medium text-gray-600 mb-2">Category</label>
                    <select id="categoryFilter" onchange="filterBooks()" class="w-full px-4 py-2 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none">
                        <option value="all">All Categories</option>
                        <option value="Reference">Reference Books</option>
                        <option value="Mathematics">Mathematics</option>
                        <option value="Physics">Physics</option>
                        <option value="Sample Papers">Sample Papers</option>
                        <option value="PYQs">Previous Year Questions</option>
                        <option value="English">English</option>
                    </select>
                </div>

                <button onclick="resetFilters()" class="px-6 py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 transition-colors self-end">
                    Reset
                </button>
            </div>
        </div>

        <!-- Recently Viewed -->
        <div id="recentSection" class="mb-8 hidden">
            <h3 class="text-xl font-bold text-gray-800 mb-4 flex items-center gap-2">
                <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                Recently Viewed
            </h3>
            <div id="recentBooks" class="flex gap-4 overflow-x-auto pb-4"></div>
        </div>

        <!-- Books Count -->
        <div class="mb-6">
            <h3 class="text-xl font-bold text-gray-800 mb-4 flex items-center gap-2">
                <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"></path>
                </svg>
                All Books (<span id="bookCount">6</span>)
            </h3>
        </div>

        <!-- Books Grid -->
        <div id="booksGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6"></div>

        <!-- No Results -->
        <div id="noResults" class="text-center py-16 hidden">
            <svg class="w-16 h-16 text-gray-300 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"></path>
            </svg>
            <h3 class="text-xl font-semibold text-gray-600 mb-2">No books found</h3>
            <p class="text-gray-500">Try adjusting your search or filters</p>
        </div>
    </div>

    <!-- Loading Modal -->
    <div id="loadingModal" class="loading">
        <div class="bg-white rounded-xl p-8 text-center">
            <div class="spinner mx-auto mb-4"></div>
            <p class="text-gray-700 font-medium">Preparing your download...</p>
        </div>
    </div>

    <!-- Book Preview Modal -->
    <div id="bookModal" class="modal" onclick="closeModal(event)">
        <div class="bg-white rounded-2xl max-w-2xl w-full max-h-[90vh] overflow-auto" onclick="event.stopPropagation()">
            <div class="p-6">
                <div class="flex items-start justify-between mb-6">
                    <div>
                        <h3 id="modalTitle" class="text-2xl font-bold text-gray-800 mb-2"></h3>
                        <p id="modalAuthor" class="text-gray-600"></p>
                    </div>
                    <button onclick="closeModal()" class="p-2 hover:bg-gray-100 rounded-full transition-colors">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                        </svg>
                    </button>
                </div>

                <img id="modalImage" class="w-full h-96 object-cover rounded-xl mb-6" />

                <div class="grid grid-cols-2 gap-4 mb-6">
                    <div class="bg-gray-50 p-4 rounded-lg">
                        <p class="text-sm text-gray-600 mb-1">Class</p>
                        <p id="modalClass" class="font-semibold text-gray-800"></p>
                    </div>
                    <div class="bg-gray-50 p-4 rounded-lg">
                        <p class="text-sm text-gray-600 mb-1">Edition</p>
                        <p id="modalEdition" class="font-semibold text-gray-800"></p>
                    </div>
                    <div class="bg-gray-50 p-4 rounded-lg">
                        <p class="text-sm text-gray-600 mb-1">Rating</p>
                        <p id="modalRating" class="font-semibold text-gray-800 flex items-center gap-1">
                            <svg class="w-4 h-4 fill-yellow-400 text-yellow-400" viewBox="0 0 24 24">
                                <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"></path>
                            </svg>
                            <span id="modalRatingValue"></span>
                        </p>
                    </div>
                    <div class="bg-gray-50 p-4 rounded-lg">
                        <p class="text-sm text-gray-600 mb-1">Downloads</p>
                        <p id="modalDownloads" class="font-semibold text-gray-800"></p>
                    </div>
                </div>

                <button onclick="downloadBook(currentBook)" class="w-full px-6 py-3 bg-blue-600 text-white rounded-xl hover:bg-blue-700 transition-colors font-medium flex items-center justify-center gap-2">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                    </svg>
                    Download PDF
                </button>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white mt-16 py-8">
        <div class="max-w-7xl mx-auto px-4 text-center">
            <p class="text-gray-400">Made with ❤️ by Bhavesh</p>
            <p class="text-gray-500 text-sm mt-2">© 2025 BOOKStore. All rights reserved.</p>
        </div>
    </footer>

    <script>
        const books = [
            {
                id: 1,
                title: "Brahmastra Booklet",
                class: "X",
                category: "Reference",
                author: "Next Toppers",
                edition: "2025-2026",
                rating: 4.8,
                downloads: 15420,
                image: "https://images.unsplash.com/photo-1543002588-bfa74002ed7e?w=300&h=400&fit=crop",
                price: "Free"
            },
            {
                id: 2,
                title: "RD Sharma",
                class: "X",
                category: "Mathematics",
                author: "RD Sharma",
                edition: "2023-2024",
                rating: 4.6,
                downloads: 28500,
                image: "https://images.unsplash.com/photo-1532012197267-da84d127e765?w=300&h=400&fit=crop",
                price: "Free"
            },
            {
                id: 3,
                title: "NCERT Physics",
                class: "XII",
                category: "Physics",
                author: "NCERT",
                edition: "2024-2025",
                rating: 4.9,
                downloads: 45200,
                image: "https://images.unsplash.com/photo-1589998059171-988d887df646?w=300&h=400&fit=crop",
                price: "Free"
            },
            {
                id: 4,
                title: "Oswaal Sample Papers",
                class: "XII",
                category: "Sample Papers",
                author: "Oswaal",
                edition: "2025",
                rating: 4.7,
                downloads: 32100,
                image: "https://images.unsplash.com/photo-1481627834876-b7833e8f5570?w=300&h=400&fit=crop",
                price: "Free"
            },
            {
                id: 5,
                title: "Chemistry PYQs",
                class: "XII",
                category: "PYQs",
                author: "CBSE",
                edition: "2024",
                rating: 4.5,
                downloads: 18900,
                image: "https://images.unsplash.com/photo-1532153955177-f59af40d6472?w=300&h=400&fit=crop",
                price: "Free"
            },
            {
                id: 6,
                title: "English Literature",
                class: "X",
                category: "English",
                author: "NCERT",
                edition: "2024-2025",
                rating: 4.4,
                downloads: 22300,
                image: "https://images.unsplash.com/photo-1512820790803-83ca734da794?w=300&h=400&fit=crop",
                price: "Free"
            }
        ];

        let favorites = [];
        let recentViews = [];
        let currentBook = null;

        function renderBooks(filteredBooks) {
            const grid = document.getElementById('booksGrid');
            const noResults = document.getElementById('noResults');
            const bookCount = document.getElementById('bookCount');

            bookCount.textContent = filteredBooks.length;

            if (filteredBooks.length === 0) {
                grid.innerHTML = '';
                noResults.classList.remove('hidden');
                return;
            }

            noResults.classList.add('hidden');
            
            grid.innerHTML = filteredBooks.map(book => `
                <div class="book-card bg-white rounded-xl shadow-md overflow-hidden">
                    <div class="relative">
                        <img src="${book.image}" alt="${book.title}" class="w-full h-64 object-cover" />
                        <button onclick="toggleFavorite(${book.id})" class="absolute top-3 right-3 p-2 bg-white/90 rounded-full hover:bg-white transition-colors shadow-lg">
                            <svg class="w-5 h-5 ${favorites.includes(book.id) ? 'fill-red-500 text-red-500' : 'text-gray-600'}" fill="${favorites.includes(book.id) ? 'currentColor' : 'none'}" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"></path>
                            </svg>
                        </button>
                        <div class="absolute bottom-3 left-3 px-3 py-1 bg-blue-600 text-white text-sm font-medium rounded-full">
                            ${book.price}
                        </div>
                    </div>

                    <div class="p-5">
                        <div class="flex items-center justify-between mb-2">
                            <span class="text-xs font-semibold text-blue-600 bg-blue-50 px-2 py-1 rounded">
                                Class ${book.class}
                            </span>
                            <span class="text-xs text-gray-500">${book.category}</span>
                        </div>

                        <h4 class="font-bold text-lg text-gray-800 mb-1 truncate">${book.title}</h4>
                        <p class="text-sm text-gray-600 mb-3">by ${book.author}</p>

                        <div class="flex items-center gap-4 mb-4 text-sm text-gray-600">
                            <div class="flex items-center gap-1">
                                <svg class="w-4 h-4 fill-yellow-400 text-yellow-400" viewBox="0 0 24 24">
                                    <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"></path>
                                </svg>
                                <span class="font-medium">${book.rating}</span>
                            </div>
                            <div class="flex items-center gap-1">
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                                </svg>
                                <span>${(book.downloads / 1000).toFixed(1)}K</span>
                            </div>
                        </div>

                        <div class="flex gap-2">
                            <button onclick="previewBook(${book.id})" class="flex-1 px-4 py-2 border-2 border-blue-600 text-blue-600 rounded-lg hover:bg-blue-50 transition-colors font-medium">
                                Preview
                            </button>
                            <button onclick="downloadBook(books[${book.id - 1}])" class="flex-1 px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors font-medium flex items-center justify-center gap-2">
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                                </svg>
                                Download
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function filterBooks() {
            const searchQuery = document.getElementById('searchInput').value.toLowerCase();
            const selectedClass = document.getElementById('classFilter').value;
            const selectedCategory = document.getElementById('categoryFilter').value;

            const filtered = books.filter(book => {
                const matchesSearch = book.title.toLowerCase().includes(searchQuery) ||
                                    book.author.toLowerCase().includes(searchQuery);
                const matchesClass = selectedClass === 'all' || book.class === selectedClass;
                const matchesCategory = selectedCategory === 'all' || book.category === selectedCategory;
                return matchesSearch && matchesClass && matchesCategory;
            });

            renderBooks(filtered);
        }

        function resetFilters() {
            document.getElementById('searchInput').value = '';
            document.getElementById('classFilter').value = 'all';
            document.getElementById('categoryFilter').value = 'all';
            filterBooks();
        }

        function toggleFilters() {
            const section = document.getElementById('filterSection');
            const text = document.getElementById('filterToggleText');
            const chevron = document.getElementById('filterChevron');
            
            section.classList.toggle('hidden');
            text.textContent = section.classList.contains('hidden') ? 'Show' : 'Hide';
            chevron.classList.toggle('rotate-180');
        }

        function toggleFavorite(bookId) {
            if (favorites.includes(bookId)) {
                favorites = favorites.filter(id => id !== bookId);
            } else {
                favorites.push(bookId);
            }
            filterBooks();
        }

        function previewBook(bookId) {
            const book = books.find(b => b.id === bookId);
            currentBook = book;
            
            if (!recentViews.find(b => b.id === bookId)) {
                recentViews = [book, ...recentViews.slice(0, 4)];
                renderRecentViews();
            }

            document.getElementById('modalTitle').textContent = book.title;
            document.getElementById('modalAuthor').textContent = 'by ' + book.author;
            document.getElementById('modalImage').src = book.image;
            document.getElementById('modalClass').textContent = book.class;
            document.getElementById('modalEdition').textContent = book.edition;
            document.getElementById('modalRatingValue').textContent = book.rating;
            document.getElementById('modalDownloads').textContent = book.downloads.toLocaleString();
            
            document.getElementById('bookModal').classList.add('active');
        }

        function closeModal(event) {
            if (!event || event.target.id === 'bookModal') {
                document.getElementById('bookModal').classList.remove('active');
            }
        }

        function downloadBook(book) {
            const loading = document.getElementById('loadingModal');
            loading.classList.add('active');
            
            setTimeout(() => {
                loading.classList.remove('active');
                alert(`Downloading ${book.title}...`);
                closeModal();
            }, 2000);
        }

        function renderRecentViews() {
            const section = document.getElementById('recentSection');
            const container = document.getElementById('recentBooks');
            
            if (recentViews.length === 0) {
                section.classList.add('hidden');
                return;
            }
            
            section.classList.remove('hidden');
            container.innerHTML = recentViews.map(book => `
                <div onclick="previewBook(${book.id})" class="flex-shrink-0 w-32 cursor-pointer hover:scale-105 transition-transform">
                    <img src="${book.image}" alt="${book.title}" class="w-full h-40 object-cover rounded-lg shadow-md" />
                    <p class="text-sm font-medium text-gray-700 mt-2 truncate"
