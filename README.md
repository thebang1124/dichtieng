# d-ch-
dichede.github.io
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trình Dịch Tiếng Ê-đê</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Be Vietnam Pro', sans-serif;
            background-color: #f0f4f8;
        }
        .card {
            background-color: rgba(255, 255, 255, 0.8);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .tab-button.active {
            border-color: #2563eb;
            color: #2563eb;
            background-color: #dbeafe;
        }
        .loader {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #3498db;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .dictionary-item:hover {
            background-color: #f9fafb;
            transform: translateX(4px);
        }
    </style>
</head>
<body class="antialiased text-slate-800">

    <div class="min-h-screen p-4 sm:p-6 md:p-8 flex flex-col items-center">
        <header class="text-center mb-8">
            <h1 class="text-4xl sm:text-5xl font-bold text-slate-900">Trình Dịch Tiếng Ê-đê</h1>
            <p class="mt-2 text-lg text-slate-600">Một công cụ hiện đại để khám phá ngôn ngữ Ê-đê</p>
        </header>

        <main class="w-full max-w-4xl mx-auto">
            <div class="card rounded-2xl shadow-lg p-6 md:p-8">
                <p class="mb-6 text-slate-700 text-center">
                    Ứng dụng này cho phép bạn dịch văn bản, tạo ví dụ, tóm tắt nội dung và thậm chí dịch từ hình ảnh. Bắt đầu bằng cách nhập văn bản vào ô bên dưới.
                </p>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="flex flex-col space-y-4">
                        <label for="inputText" class="font-semibold text-slate-800">Văn bản gốc (Việt hoặc Ê-đê)</label>
                        <div class="relative w-full">
                            <textarea id="inputText" rows="8" class="w-full p-4 rounded-lg border-2 border-slate-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-300 resize-none" placeholder="Nhập văn bản cần dịch..."></textarea>
                            <button id="recordButton" title="Ghi âm giọng nói" class="absolute bottom-3 right-3 p-2 rounded-full bg-slate-100 hover:bg-slate-200 transition">
                                <span class="record-icon">🎙️</span>
                            </button>
                        </div>
                    </div>
                    <div class="flex flex-col space-y-4">
                        <label for="outputText" class="font-semibold text-slate-800">Kết quả dịch</label>
                         <div class="relative w-full">
                            <textarea id="outputText" rows="8" readonly class="w-full p-4 rounded-lg bg-slate-100 border-2 border-slate-200 resize-none" placeholder="Kết quả dịch sẽ hiển thị ở đây..."></textarea>
                            <button id="speakTranslatedTextButton" title="Phát âm văn bản" class="absolute bottom-3 right-3 p-2 rounded-full bg-slate-200 hover:bg-slate-300 transition">
                                <span>🔊</span>
                            </button>
                        </div>
                    </div>
                </div>

                <div class="mt-6 flex flex-col sm:flex-row items-center justify-center gap-4">
                    <button id="translateButton" class="w-full sm:w-auto flex items-center justify-center gap-2 px-8 py-3 bg-blue-600 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition-transform transform hover:scale-105">
                        <span class="button-icon">✨</span>
                        <span class="button-text">Dịch</span>
                    </button>
                    <button id="generateExamplesButton" class="w-full sm:w-auto flex items-center justify-center gap-2 px-6 py-3 bg-orange-500 text-white font-semibold rounded-lg shadow-md hover:bg-orange-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-orange-500 transition-transform transform hover:scale-105">
                        <span class="button-icon">💡</span>
                        <span class="button-text">Tạo ví dụ</span>
                    </button>
                    <button id="summarizeExplainButton" class="w-full sm:w-auto flex items-center justify-center gap-2 px-6 py-3 bg-purple-600 text-white font-semibold rounded-lg shadow-md hover:bg-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-500 transition-transform transform hover:scale-105">
                        <span class="button-icon">📝</span>
                        <span class="button-text">Tóm tắt</span>
                    </button>
                </div>
                 <div id="additionalOutputWrapper" class="mt-6 hidden">
                    <label for="additionalOutput" class="font-semibold text-slate-800">Kết quả bổ sung</label>
                    <div class="relative w-full mt-2">
                        <textarea id="additionalOutput" rows="4" readonly class="w-full p-4 rounded-lg bg-slate-100 border-2 border-slate-200 resize-none"></textarea>
                        <button id="speakAdditionalTextButton" title="Phát âm văn bản" class="absolute bottom-3 right-3 p-2 rounded-full bg-slate-200 hover:bg-slate-300 transition">
                             <span>🔊</span>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Write Essay Section -->
            <div class="card rounded-2xl shadow-lg p-6 md:p-8 mt-10">
                <h2 class="text-2xl font-bold text-slate-900 mb-4 text-center">Viết Bài Văn Từ Gợi Ý</h2>
                <p class="mb-6 text-slate-700 text-center">
                    Nhập các từ khóa hoặc gợi ý của bạn vào đây, và Gemini sẽ giúp bạn tạo ra một bài văn hoàn chỉnh.
                </p>
                <div class="flex flex-col space-y-4">
                    <label for="essayKeywords" class="font-semibold text-slate-800">Từ khóa/Gợi ý:</label>
                    <textarea id="essayKeywords" rows="4" class="w-full p-4 rounded-lg border-2 border-slate-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition duration-300 resize-none" placeholder="Ví dụ: Lợi ích của việc học tiếng Ê-đê, văn hóa dân tộc, bảo tồn ngôn ngữ..."></textarea>
                </div>
                <button id="generateEssayButton" class="mt-6 w-full flex items-center justify-center gap-2 px-8 py-3 bg-indigo-600 text-white font-semibold rounded-lg shadow-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-transform transform hover:scale-105">
                    <span class="button-icon">✍️</span>
                    <span class="button-text">Tạo Bài Văn</span>
                </button>
                <div id="essayOutputWrapper" class="mt-6 hidden">
                    <label for="essayOutput" class="font-semibold text-slate-800">Bài văn đã tạo:</label>
                    <div class="relative w-full mt-2">
                        <textarea id="essayOutput" rows="10" readonly class="w-full p-4 rounded-lg bg-slate-100 border-2 border-slate-200 resize-none"></textarea>
                        <button id="speakEssayTextButton" title="Phát âm bài văn" class="absolute bottom-3 right-3 p-2 rounded-full bg-slate-200 hover:bg-slate-300 transition">
                             <span>🔊</span>
                        </button>
                    </div>
                </div>
            </div>

            <div class="mt-10">
                <div class="mb-4 border-b border-slate-300 flex justify-center">
                    <button data-tab="imageTab" class="tab-button text-lg font-medium py-2 px-6 border-b-2 transition active">Dịch từ ảnh</button>
                    <button data-tab="dictionaryTab" class="tab-button text-lg font-medium py-2 px-6 border-b-2 border-transparent text-slate-500 hover:text-slate-700 transition">Từ điển cá nhân</button>
                </div>

                <div class="tab-content card rounded-2xl shadow-lg p-6 md:p-8">
                    <div id="imageTab" class="space-y-6">
                        <p class="text-slate-700">Tải lên một hình ảnh có chứa văn bản để trích xuất và dịch. Hệ thống sẽ tự động nhận diện ngôn ngữ và thực hiện dịch thuật.</p>
                        <div class="p-6 border-2 border-dashed border-slate-300 rounded-lg text-center cursor-pointer hover:border-blue-500 hover:bg-blue-50 transition" id="dropZone">
                            <input type="file" id="imageInput" class="hidden" accept="image/*">
                            <div id="imagePlaceholder">
                                <span class="text-4xl">🖼️</span>
                                <p class="mt-2 text-slate-600">Kéo và thả ảnh vào đây, hoặc <span class="font-semibold text-blue-600">nhấn để chọn file</span></p>
                            </div>
                            <div id="imagePreviewWrapper" class="hidden relative">
                                <img id="imagePreview" class="max-h-60 mx-auto rounded-md shadow-md"/>
                                <button id="removeImageButton" class="absolute -top-2 -right-2 bg-white rounded-full p-1 shadow-md text-red-500 hover:bg-red-50 text-xl font-bold">&times;</button>
                            </div>
                        </div>
                        <button id="translateImageButton" class="w-full flex items-center justify-center gap-2 px-8 py-3 bg-teal-600 text-white font-semibold rounded-lg shadow-md hover:bg-teal-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-teal-500 transition-transform transform hover:scale-105 disabled:bg-slate-400 disabled:cursor-not-allowed disabled:transform-none">
                            <span class="button-icon">📷</span>
                            <span class="button-text">Dịch từ ảnh</span>
                        </button>
                    </div>

                    <div id="dictionaryTab" class="hidden space-y-6">
                        <p class="text-slate-700">Xây dựng từ điển của riêng bạn. Các bản dịch bạn thêm vào đây sẽ được ưu tiên sử dụng, giúp cải thiện độ chính xác theo thời gian.</p>
                        <div>
                            <h3 class="text-lg font-semibold mb-3">Thêm từ mới</h3>
                            <div class="flex flex-col sm:flex-row gap-4">
                                <input type="text" id="newEdeText" placeholder="Nhập từ tiếng Ê-đê" class="flex-1 p-3 rounded-lg border-2 border-slate-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition">
                                <input type="text" id="newVietText" placeholder="Nhập nghĩa tiếng Việt" class="flex-1 p-3 rounded-lg border-2 border-slate-200 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition">
                                <button id="addTermButton" class="px-6 py-3 bg-green-600 text-white font-semibold rounded-lg shadow-md hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500 transition-transform transform hover:scale-105">Thêm</button>
                            </div>
                        </div>
                        
                        <!-- New: Load Dictionary Section -->
                        <div class="mt-6 pt-4 border-t border-slate-200">
                            <h3 class="text-lg font-semibold mb-3">Tải từ điển từ File</h3>
                            <p class="text-slate-600 text-sm mb-2">Chọn một file JSON (.json) chứa các cặp từ điển của bạn. Định dạng file: <code class="bg-slate-100 p-1 rounded">[{ "ede": "từ Ê-đê", "viet": "từ tiếng Việt" }]</code></p>
                            <div class="flex flex-col sm:flex-row gap-4 items-center">
                                <input type="file" id="loadDictionaryFileInput" accept=".json" class="flex-1 p-2 rounded-lg border-2 border-slate-200">
                                <button id="loadDictionaryFromFileButton" class="px-6 py-3 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition-transform transform hover:scale-105">
                                    <span class="button-icon">📂</span>
                                    <span class="button-text">Tải từ File</span>
                                </button>
                            </div>
                            <p class="text-slate-600 text-sm mt-4 mb-2">
                                <span class="font-bold">Lưu ý:</span> Tính năng tải từ điển từ Web (URL) hiện đang được phát triển.
                            </p>
                            <!-- Placeholder for Load from Web Button -->
                            <!--
                            <div class="flex flex-col sm:flex-row gap-4 mt-2">
                                <input type="text" id="loadDictionaryUrlInput" placeholder="https://example.com/dictionary.json" class="flex-1 p-3 rounded-lg border-2 border-slate-200">
                                <button id="loadDictionaryFromWebButton" class="px-6 py-3 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition-transform transform hover:scale-105">
                                    <span class="button-icon">🌐</span>
                                    <span class="button-text">Tải từ Web</span>
                                </button>
                            </div>
                            -->
                        </div>

                        <div class="mt-6 pt-4 border-t border-slate-200">
                            <h3 class="lg font-semibold mb-3">Các bản dịch của bạn</h3>
                            <div id="customTranslationsList" class="max-h-80 overflow-y-auto space-y-3 pr-2">
                                <p class="text-slate-500 text-center py-4" id="dictionaryPlaceholder">Từ điển cá nhân của bạn đang trống.</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>
        
        <footer class="text-center mt-10 text-slate-500 text-sm">
            <p>Phát triển bởi Gemini &copy; 2025</p>
            <p id="userIdDisplay" class="mt-1 opacity-70">Đang chờ xác thực người dùng...</p>
        </footer>
    </div>

<script>
document.addEventListener('DOMContentLoaded', () => {

    const state = {
        isLoading: false,
        currentTab: 'imageTab',
        userId: null,
        dictionary: [
            { id: 1, ede: 'klei', viet: 'lời nói' },
            { id: 2, ede: 'mnuih', viet: 'người' },
            { id: 3, ede: 'hriê', viet: 'ngày' }
        ],
        selectedImageFile: null,
        isGeneratingEssay: false
    };

    const ui = {
        inputText: document.getElementById('inputText'),
        outputText: document.getElementById('outputText'),
        additionalOutput: document.getElementById('additionalOutput'),
        additionalOutputWrapper: document.getElementById('additionalOutputWrapper'),
        translateButton: document.getElementById('translateButton'),
        generateExamplesButton: document.getElementById('generateExamplesButton'),
        summarizeExplainButton: document.getElementById('summarizeExplainButton'),
        recordButton: document.getElementById('recordButton'),
        speakTranslatedTextButton: document.getElementById('speakTranslatedTextButton'),
        speakAdditionalTextButton: document.getElementById('speakAdditionalTextButton'),
        tabs: document.querySelectorAll('.tab-button'),
        tabContents: document.querySelectorAll('.tab-content > div'),
        imageInput: document.getElementById('imageInput'),
        dropZone: document.getElementById('dropZone'),
        imagePlaceholder: document.getElementById('imagePlaceholder'),
        imagePreviewWrapper: document.getElementById('imagePreviewWrapper'),
        imagePreview: document.getElementById('imagePreview'),
        removeImageButton: document.getElementById('removeImageButton'),
        translateImageButton: document.getElementById('translateImageButton'),
        newEdeText: document.getElementById('newEdeText'),
        newVietText: document.getElementById('newVietText'),
        addTermButton: document.getElementById('addTermButton'),
        customTranslationsList: document.getElementById('customTranslationsList'),
        dictionaryPlaceholder: document.getElementById('dictionaryPlaceholder'),
        userIdDisplay: document.getElementById('userIdDisplay'),
        // New elements for essay generation
        essayKeywords: document.getElementById('essayKeywords'),
        generateEssayButton: document.getElementById('generateEssayButton'),
        essayOutput: document.getElementById('essayOutput'),
        essayOutputWrapper: document.getElementById('essayOutputWrapper'),
        speakEssayTextButton: document.getElementById('speakEssayTextButton'),
        // New elements for dictionary loading
        loadDictionaryFileInput: document.getElementById('loadDictionaryFileInput'),
        loadDictionaryFromFileButton: document.getElementById('loadDictionaryFromFileButton'),
        // loadDictionaryUrlInput: document.getElementById('loadDictionaryUrlInput'), // Placeholder
        // loadDictionaryFromWebButton: document.getElementById('loadDictionaryFromWebButton') // Placeholder
    };
    
    // Function to call Gemini API
    async function callGeminiAPI(prompt, imageData = null, model = 'gemini-2.0-flash') {
        const apiKey = ""; // API key will be provided by the Canvas environment automatically
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${model}:generateContent?key=${apiKey}`;

        let chatHistory = [];
        let parts = [{ text: prompt }];

        if (imageData) {
            parts.push({
                inlineData: {
                    mimeType: imageData.mimeType,
                    data: imageData.data
                }
            });
        }
        chatHistory.push({ role: "user", parts: parts });

        const payload = { contents: chatHistory };

        try {
            const response = await fetch(apiUrl, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(payload)
            });

            if (!response.ok) {
                const errorData = await response.json();
                console.error("API Error:", errorData);
                throw new Error(`Lỗi API: ${response.status} - ${errorData.error.message || 'Unknown error'}`);
            }

            const result = await response.json();
            if (result.candidates && result.candidates.length > 0 &&
                result.candidates[0].content && result.candidates[0].content.parts &&
                result.candidates[0].content.parts.length > 0) {
                return result.candidates[0].content.parts[0].text;
            } else {
                console.warn("Unexpected API response structure:", result);
                throw new Error("Cấu trúc phản hồi API không mong muốn.");
            }
        } catch (error) {
            console.error("Error calling Gemini API:", error);
            throw error;
        }
    }

    function setLoadingState(button, isLoading, originalText) {
        const textSpan = button.querySelector('.button-text');
        const iconSpan = button.querySelector('.button-icon');
        
        if (isLoading) {
            state.isLoading = true; // Global loading state
            button.disabled = true;
            textSpan.textContent = 'Đang xử lý...';
            iconSpan.innerHTML = '<div class="loader"></div>';
        } else {
            state.isLoading = false; // Global loading state
            button.disabled = false;
            textSpan.textContent = originalText;
            switch(originalText) {
                case 'Dịch': iconSpan.innerHTML = '✨'; break;
                case 'Tạo ví dụ': iconSpan.innerHTML = '💡'; break;
                case 'Tóm tắt': iconSpan.innerHTML = '📝'; break;
                case 'Dịch từ ảnh': iconSpan.innerHTML = '📷'; break;
                case 'Tạo Bài Văn': iconSpan.innerHTML = '✍️'; break; // New icon for essay button
                case 'Tải từ File': iconSpan.innerHTML = '📂'; break; // New icon for load file button
                // case 'Tải từ Web': iconSpan.innerHTML = '🌐'; break; // Placeholder
            }
        }
    }
    
    function renderDictionary() {
        ui.customTranslationsList.innerHTML = '';
        if (state.dictionary.length === 0) {
            ui.customTranslationsList.appendChild(ui.dictionaryPlaceholder);
            ui.dictionaryPlaceholder.classList.remove('hidden');
        } else {
            if (ui.dictionaryPlaceholder) {
                ui.dictionaryPlaceholder.classList.add('hidden');
            }
            state.dictionary.forEach(term => {
                const item = document.createElement('div');
                item.className = 'dictionary-item flex justify-between items-center p-3 rounded-lg border border-slate-200 transition-all duration-300';
                item.innerHTML = `
                    <div>
                        <p class="font-semibold text-slate-800">${term.ede}</p>
                        <p class="text-sm text-slate-500">${term.viet}</p>
                    </div>
                    <button data-id="${term.id}" class="delete-term-btn text-red-500 hover:text-red-700 p-1 rounded-full text-lg">&times;</button>
                `;
                ui.customTranslationsList.appendChild(item);
            });
        }
    }

    async function handleTranslate() {
        if (state.isLoading || !ui.inputText.value.trim()) return;
        setLoadingState(ui.translateButton, true, 'Dịch');
        ui.outputText.value = '';
        ui.additionalOutputWrapper.classList.add('hidden');
        
        const inputTextLower = ui.inputText.value.trim().toLowerCase();
        let translatedText = '';

        const customMatch = state.dictionary.find(t => t.ede.toLowerCase() === inputTextLower || t.viet.toLowerCase() === inputTextLower);
        if (customMatch) {
            translatedText = customMatch.ede.toLowerCase() === inputTextLower ? customMatch.viet : customMatch.ede;
            translatedText += " (từ từ điển cá nhân)";
            ui.outputText.value = translatedText;
            setLoadingState(ui.translateButton, false, 'Dịch');
            return;
        }
        
        const prompt = `Bạn là một công cụ dịch thuật chuyên nghiệp. Hãy dịch văn bản sau đây giữa tiếng Việt và tiếng Ê-đê. Nếu văn bản là tiếng Việt, hãy dịch sang tiếng Ê-đê. Nếu văn bản là tiếng Ê-đê, hãy dịch sang tiếng Việt. Chỉ trả về văn bản đã dịch, không thêm bất kỳ giải thích nào. Văn bản cần dịch: ${ui.inputText.value}`;

        try {
            translatedText = await callGeminiAPI(prompt);
            ui.outputText.value = translatedText;
        } catch (error) {
            ui.outputText.value = `Đã xảy ra lỗi trong quá trình dịch: ${error.message}`;
        } finally {
            setLoadingState(ui.translateButton, false, 'Dịch');
        }
    }

    async function handleGenerateExamples() {
        if (state.isLoading || !ui.outputText.value.trim() || ui.outputText.value.includes("Kết quả dịch sẽ hiển thị ở đây")) return;
        setLoadingState(ui.generateExamplesButton, true, 'Tạo ví dụ');
        ui.additionalOutput.value = '';
        
        const prompt = `Tạo 3 câu ví dụ sử dụng từ hoặc cụm từ "${ui.outputText.value}" trong ngữ cảnh khác nhau. Các câu ví dụ này nên được dịch sang ngôn ngữ còn lại (nếu từ gốc là tiếng Việt, ví dụ là tiếng Ê-đê và ngược lại). Chỉ trả về các câu ví dụ, mỗi câu trên một dòng mới, không thêm bất kỳ giải thích nào.`;

        try {
            const examples = await callGeminiAPI(prompt);
            ui.additionalOutput.value = examples;
            ui.additionalOutputWrapper.classList.remove('hidden');
        } catch (error) {
            ui.additionalOutput.value = `Đã xảy ra lỗi khi tạo ví dụ: ${error.message}`;
        } finally {
            setLoadingState(ui.generateExamplesButton, false, 'Tạo ví dụ');
        }
    }

    async function handleSummarize() {
        if (state.isLoading || !ui.outputText.value.trim() || ui.outputText.value.includes("Kết quả dịch sẽ hiển thị ở đây")) return;
        setLoadingState(ui.summarizeExplainButton, true, 'Tóm tắt');
        ui.additionalOutput.value = '';

        const prompt = `Tóm tắt hoặc giải thích ngắn gọn ý nghĩa của văn bản sau: "${ui.outputText.value}". Nếu văn bản phức tạp, hãy giải thích các điểm chính. Chỉ trả về phần tóm tắt/giải thích, không thêm bất kỳ giải thích nào khác.`;

        try {
            const summary = await callGeminiAPI(prompt);
            ui.additionalOutput.value = summary;
            ui.additionalOutputWrapper.classList.remove('hidden');
        } catch (error) {
            ui.additionalOutput.value = `Đã xảy ra lỗi khi tóm tắt/giải thích: ${error.message}`;
        } finally {
            setLoadingState(ui.summarizeExplainButton, false, 'Tóm tắt');
        }
    }

    async function handleGenerateEssay() {
        if (state.isLoading || !ui.essayKeywords.value.trim()) return;
        setLoadingState(ui.generateEssayButton, true, 'Tạo Bài Văn');
        ui.essayOutput.value = '';
        ui.essayOutputWrapper.classList.add('hidden');

        const prompt = `Viết một bài văn về chủ đề dựa trên các từ khóa sau: "${ui.essayKeywords.value}". Bài văn nên có độ dài vừa phải, khoảng 200-300 từ, và có cấu trúc rõ ràng (mở bài, thân bài, kết luận).`;

        try {
            const essay = await callGeminiAPI(prompt);
            ui.essayOutput.value = essay;
            ui.essayOutputWrapper.classList.remove('hidden');
        } catch (error) {
            ui.essayOutput.value = `Đã xảy ra lỗi khi tạo bài văn: ${error.message}`;
        } finally {
            setLoadingState(ui.generateEssayButton, false, 'Tạo Bài Văn');
        }
    }
    
    function setupTabs() {
        ui.tabs.forEach(button => {
            button.addEventListener('click', () => {
                const tabId = button.dataset.tab;
                if (tabId === state.currentTab) return;

                ui.tabs.forEach(btn => btn.classList.remove('active'));
                button.classList.add('active');

                ui.tabContents.forEach(content => content.classList.add('hidden'));
                document.getElementById(tabId).classList.remove('hidden');
                
                state.currentTab = tabId;
            });
        });
    }

    function handleImageSelection(file) {
        if (file && file.type.startsWith('image/')) {
            state.selectedImageFile = file;
            const reader = new FileReader();
            reader.onload = (e) => {
                ui.imagePreview.src = e.target.result;
                ui.imagePlaceholder.classList.add('hidden');
                ui.imagePreviewWrapper.classList.remove('hidden');
                ui.translateImageButton.disabled = false;
            };
            reader.readAsDataURL(file);
        }
    }

    async function handleTranslateImage() {
        if(state.isLoading || !state.selectedImageFile) return;
        setLoadingState(ui.translateImageButton, true, 'Dịch từ ảnh');
        ui.outputText.value = '';
        ui.additionalOutputWrapper.classList.add('hidden');

        const reader = new FileReader();
        reader.onloadend = async () => {
            const base64Image = reader.result.split(',')[1];
            const mimeType = state.selectedImageFile.type;

            const prompt = `Trích xuất tất cả văn bản từ hình ảnh này. Sau đó, nếu văn bản đã trích xuất là tiếng Ê-đê, hãy dịch sang tiếng Việt. Nếu văn bản đã trích xuất là tiếng Việt, hãy dịch sang tiếng Ê-đê. Nếu không phải cả hai, chỉ cung cấp văn bản đã trích xuất. Chỉ xuất ra văn bản đã dịch hoặc văn bản đã trích xuất nếu không thể dịch. Không thêm bất kỳ lời giải thích nào khác.`;
            
            try {
                const translatedText = await callGeminiAPI(prompt, { data: base64Image, mimeType: mimeType });
                ui.outputText.value = translatedText;
            } catch (error) {
                ui.outputText.value = `Đã xảy ra lỗi khi dịch từ ảnh: ${error.message}`;
            } finally {
                setLoadingState(ui.translateImageButton, false, 'Dịch từ ảnh');
            }
        };
        reader.readAsDataURL(state.selectedImageFile);
    }
    
    function handleAddTerm() {
        const ede = ui.newEdeText.value.trim();
        const viet = ui.newVietText.value.trim();
        if (ede && viet) {
            state.dictionary.push({ id: Date.now(), ede, viet });
            renderDictionary();
            ui.newEdeText.value = '';
            ui.newVietText.value = '';
        }
    }

    function handleDeleteTerm(e) {
        if (e.target.classList.contains('delete-term-btn')) {
            const id = parseInt(e.target.dataset.id);
            state.dictionary = state.dictionary.filter(term => term.id !== id);
            renderDictionary();
        }
    }

    async function handleLoadDictionaryFromFile() {
        const file = ui.loadDictionaryFileInput.files[0];
        if (!file) {
            alert("Vui lòng chọn một file JSON để tải.");
            return;
        }

        setLoadingState(ui.loadDictionaryFromFileButton, true, 'Tải từ File');

        const reader = new FileReader();
        reader.onload = (e) => {
            try {
                const loadedData = JSON.parse(e.target.result);
                if (Array.isArray(loadedData) && loadedData.every(item => item.ede && item.viet)) {
                    // Filter out duplicates and add new IDs
                    const newEntries = loadedData.filter(newItem => 
                        !state.dictionary.some(existingItem => 
                            existingItem.ede.toLowerCase() === newItem.ede.toLowerCase() && 
                            existingItem.viet.toLowerCase() === newItem.viet.toLowerCase()
                        )
                    ).map(item => ({ id: Date.now() + Math.random(), ...item })); // Add unique ID

                    state.dictionary = [...state.dictionary, ...newEntries];
                    renderDictionary();
                    alert(`Đã tải thành công ${newEntries.length} từ vào từ điển!`);
                } else {
                    alert("Định dạng file JSON không hợp lệ. Vui lòng đảm bảo file chứa mảng các đối tượng có thuộc tính 'ede' và 'viet'.");
                }
            } catch (error) {
                alert(`Lỗi khi đọc file: ${error.message}. Vui lòng đảm bảo đây là file JSON hợp lệ.`);
                console.error("Error parsing dictionary file:", error);
            } finally {
                setLoadingState(ui.loadDictionaryFromFileButton, false, 'Tải từ File');
            }
        };
        reader.onerror = () => {
            alert("Không thể đọc file.");
            setLoadingState(ui.loadDictionaryFromFileButton, false, 'Tải từ File');
        };
        reader.readAsText(file);
    }

    // Placeholder for handleLoadDictionaryFromWeb (due to CORS in single HTML file)
    // async function handleLoadDictionaryFromWeb() {
    //     alert("Tính năng tải từ điển từ Web đang được phát triển và có thể yêu cầu một backend server để xử lý CORS.");
    // }


    ui.translateButton.addEventListener('click', handleTranslate);
    ui.generateExamplesButton.addEventListener('click', handleGenerateExamples);
    ui.summarizeExplainButton.addEventListener('click', handleSummarize);
    ui.generateEssayButton.addEventListener('click', handleGenerateEssay);
    ui.addTermButton.addEventListener('click', handleAddTerm);
    ui.customTranslationsList.addEventListener('click', handleDeleteTerm);
    ui.translateImageButton.addEventListener('click', handleTranslateImage);
    ui.loadDictionaryFromFileButton.addEventListener('click', handleLoadDictionaryFromFile); // New event listener
    // ui.loadDictionaryFromWebButton.addEventListener('click', handleLoadDictionaryFromWeb); // Placeholder

    ui.dropZone.addEventListener('click', () => ui.imageInput.click());
    ui.imageInput.addEventListener('change', (e) => handleImageSelection(e.target.files[0]));
    ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(eventName => {
        ui.dropZone.addEventListener(eventName, (e) => {
            e.preventDefault();
            e.stopPropagation();
        }, false);
    });
    ['dragenter', 'dragover'].forEach(eventName => {
        ui.dropZone.addEventListener(eventName, () => ui.dropZone.classList.add('bg-blue-100'), false);
    });
    ['dragleave', 'drop'].forEach(eventName => {
        ui.dropZone.addEventListener(eventName, () => ui.dropZone.classList.remove('bg-blue-100'), false);
    });
    ui.dropZone.addEventListener('drop', (e) => handleImageSelection(e.dataTransfer.files[0]));
    
    ui.removeImageButton.addEventListener('click', () => {
        state.selectedImageFile = null;
        ui.imageInput.value = '';
        ui.imagePlaceholder.classList.remove('hidden');
        ui.imagePreviewWrapper.classList.add('hidden');
        ui.translateImageButton.disabled = true;
    });
    
    // Web Speech API (Placeholders for now, not LLM-powered directly)
    ui.recordButton.addEventListener('click', () => {
        alert('Tính năng ghi âm giọng nói đang được phát triển!');
    });
    ui.speakTranslatedTextButton.addEventListener('click', () => {
        alert('Tính năng phát âm đang được phát triển!');
    });
    ui.speakAdditionalTextButton.addEventListener('click', () => {
        alert('Tính năng phát âm đang được phát triển!');
    });
    ui.speakEssayTextButton.addEventListener('click', () => {
        alert('Tính năng phát âm đang được phát triển!');
    });

    function initializeApp() {
        state.userId = `user_${Math.random().toString(36).substr(2, 9)}`;
        ui.userIdDisplay.textContent = `ID Người dùng: ${state.userId}`;
        ui.translateImageButton.disabled = true;
        setupTabs();
        renderDictionary();
    }
    
    initializeApp();
});
</script>
</body>
</html>
