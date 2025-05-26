# Daark Note

\<!DOCTYPE html\>

\<html lang="en"\>

\<head\>

\<meta charset="UTF-8"\>

\<title\>DarkNote App with ChatGPT Integration\</title\>

\<style\>

/\* Reset Styles \*/

\* {

margin: 0;

padding: 0;

box-sizing: border-box;

}

/\* Body Styles \*/

body {

font-family: "Palatino Linotype", "PT Serif", Palatino, serif;

background: linear-gradient(to bottom, #141416, #171719, #222224, #161618);

color: #e0e0e0;

margin: 0;

padding: 15px;

height: 100vh;

display: flex;

flex-direction: column;

}

/\* Container Styles \*/

.container {

display: flex;

gap: 20px;

flex-grow: 1;

overflow: hidden;

}

/\* Saved Notes Sidebar \*/

.saved-notes {

width: 250px;

min-width: 250px;

background: linear-gradient(to bottom, #010101, #262628, #111113, #161618);

padding: 10px;

border-radius: 5px;

overflow-y: auto;

box-shadow: inset 0 2px 4px rgba(0,0,0,0.1), 0 1px 2px rgba(255,255,255,0.05);

}

.saved-notes h1 {

text-align: center;

margin-bottom: 15px;

font-size: 24px;

}

/\* Search Input \*/

.recent-notes input[type="text"] {

width: 100%;

padding: 8px;

margin-bottom: 15px;

border: 1px solid #333;

border-radius: 5px;

background: #2a2a2a;

color: #e0e0e0;

font-size: 14px;

}

/\* Category Styles \*/

.category {

margin-bottom: 10px;

}

.category-header {

background-color: #2c2c2c;

padding: 5px;

border-radius: 3px;

cursor: pointer;

font-weight: bold;

font-size: 16px;

}

.category-notes {

display: none;

padding-left: 10px;

margin-top: 5px;

}

.category-notes .saved-note {

background-color: #2a2a2a;

padding: 5px;

margin-top: 5px;

border-radius: 3px;

cursor: pointer;

font-size: 14px;

}

.category-notes .saved-note:hover {

background-color: 3a3a3a;

}

/\* Main Content Styles \*/

.main-content {

flex-grow: 1;

display: flex;

flex-direction: column;

padding: 20px;

overflow-y: auto;

}

/\* Editor and Preview \*/

.editor-preview {

display: flex;

gap: 20px;

flex-grow: 1;

overflow: hidden;

min-height: 0;

transition: height 0.3s ease;

}

.editor {

flex: 1;

display: flex;

flex-direction: column;

transition: flex 0.3s ease;

}

/\* Input Fields \*/

input[type="text"], textarea, select {

width: 100%;

background: linear-gradient(to bottom, #171718, #242425, #181819, #131314);

color: #e0e0e0;

border: 1px solid #333;

padding: 10px;

border-radius: 5px;

margin-bottom: 10px;

box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);

font-family: "Palatino Linotype", "Book Antiqua", "Palatino", serif;

font-size: 16px;

}

input[type="text"]#titleInput,

input[type="text"]#tagInput,

input[type="text"]#customPromptInput {

height: 40px;

font-size: 18px;

}

textarea#noteInput {

flex-grow: 1;

resize: vertical;

height: 150px;

font-size: 18px;

}

/\* Select Dropdown \*/

select#aiActionSelect {

height: 40px;

font-size: 16px;

background: #2a2a2a;

color: #e0e0e0;

border: 1px solid #333;

}

/\* Character Count \*/

#charCount {

margin-bottom: 10px;

font-size: 14px;

color: #bbb;

}

/\* Buttons \*/

.buttons {

display: flex;

flex-wrap: wrap;

justify-content: flex-start;

margin-top: 10px;

gap: 10px;

}

.buttons button {

background-color: #242425;

color: #e0e0e0;

border: none;

padding: 10px 15px;

border-radius: 5px;

cursor: pointer;

transition: background-color 0.3s;

font-size: 14px;

}

.buttons button:hover {

background-color: #5a5a5a;

}

.buttons button:disabled {

background-color: #555;

cursor: not-allowed;

}

/\* Preview and Summary \*/

#preview, #summary, #gptPreview {

flex: 0;

background-color: #212121;

padding: 10px;

border-radius: 5px;

border-left: 1px solid #3a3a3a;

overflow-y: auto;

transition: flex 0.3s ease;

box-shadow: inset 0 2px 4px rgba(0,0,0,0.1), 0 1px 2px rgba(255,255,255,0.05);

font-size: 16px;

line-height: 1.75;

max-height: 758px;

min-height: 100px;

}

#preview h1 { font-size: 24px; }

#preview h2 { font-size: 20px; }

#preview h3 { font-size: 18px; }

#preview h4 { font-size: 16px; }

#preview h5 { font-size: 14px; }

#preview h6 { font-size: 12px; }

#preview p {

margin-top: 0;

margin-bottom: 10px;

}

#preview h1, #preview h2, #preview h3, #preview h4, #preview h5, #preview h6 {

margin-top: 0.5em;

margin-bottom: 0.3em;

line-height: 1.1;

}

#preview p {

margin-top: 0.3em;

margin-bottom: 0.3em;

}

/\* Expanded Preview \*/

.preview-visible #preview {

flex: 1;

}

/\* GPT Preview Section \*/

.gpt-preview-section {

background-color: #2a2a2a;

padding: 10px;

border-radius: 5px;

margin-top: 20px;

box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);

font-size: 16px;

line-height: 1.75;

}

.gpt-preview-section h2 {

margin-bottom: 10px;

font-size: 18px;

}

#gptResponse {

white-space: pre-wrap;

word-wrap: break-word;

}

.summary-section {

display: none;

margin-top: 20px;

background-color: #2a2a2a;

padding: 10px;

border-radius: 5px;

box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);

font-size: 16px;

line-height: 1.75;

}

.summary-section.visible {

display: block;

}

/\* Loading Indicator \*/

#loading-indicator {

text-align: center;

font-size: 18px;

color: #555;

margin-top: 10px;

}

/\* Hidden Class \*/

.hidden {

display: none;

}

/\* Footer \*/

footer {

text-align: center;

margin-top: 20px;

color: #777;

font-size: 14px;

}

/\* Taskade AI Agent Sidebar \*/

.agent-sidebar {

width: 600px;

min-width: 600px;

background-color: #212121;

border-radius: 5px;

overflow-y: auto;

transition: transform 0.3s ease;

}

.agent-sidebar.hidden {

transform: translateX(100%);

}

\</style\>

\</head\>

\<body\>

\<div class="container"\>

\<!-- Saved Notes Sidebar --\>

\<div class="saved-notes"\>

\<h1\>Dark Notes\</h1\>

\<div class="recent-notes"\>

\<input type="text" id="searchInput" placeholder="Search notes..."\>

\</div\>

\<div id="savedNotesList"\>

\<!-- Saved notes will be rendered here --\>

\</div\>

\</div\>

\<!-- Main Content Area --\>

\<div class="main-content"\>

\<!-- Editor and Preview Area --\>

\<div class="editor-preview"\>

\<div class="editor"\>

\<input type="text" id="titleInput" placeholder="Note Title"\>

\<input type="text" id="tagInput" placeholder="Tags (comma-separated)"\>

\<textarea id="noteInput" placeholder="Enter your note here..."\>\</textarea\>

\<div id="charCount"\>0 characters, 0 words\</div\>

\<!-- Custom Prompt Input --\>

\<input type="text" id="customPromptInput" placeholder="Enter custom prompt or leave blank for default"\>

\<!-- AI Action Dropdown --\>

\<label for="aiActionSelect"\>Choose an action:\</label\>

\<select id="aiActionSelect"\>

\<option value="summarize"\>Summarize\</option\>

\<option value="generateIdeas"\>Generate Novel Ideas\</option\>

\<option value="extractWisdom"\>Extract Wisdom\</option\>

\</select\>

\</div\>

\<!-- Markdown Preview --\>

\<div id="preview"\>\</div\>

\</div\>

\<!-- Summary Section --\>

\<div id="summary" class="summary-section"\>\</div\>

\<!-- GPT Preview Section --\>

\<div id="gptPreview" class="gpt-preview-section hidden"\>

\<h2\>GPT Preview\</h2\>

\<div id="gptResponse"\>\</div\>

\</div\>

\<!-- Buttons --\>

\<div class="buttons"\>

\<button id="saveButton"\>Save Note\</button\>

\<button id="clearButton"\>Clear\</button\>

\<button id="deleteButton"\>Delete Note\</button\>

\<button id="togglePreviewButton"\>MD Preview\</button\>

\<button id="toggleGPTPreviewButton"\>GPT Preview\</button\>

\<button id="exportButton"\>Export Notes\</button\>

\<button id="performAIActionButton"\>GPT\</button\>

\<!-- New Button to Toggle Taskade AI Agent Sidebar --\>

\<button id="toggleAgentSidebarButton"\>Toggle AI Agent Sidebar\</button\>

\</div\>

\</div\>

\<!-- Taskade AI Agent Sidebar (Right-Hand Sidebar) --\>

\<aside class="agent-sidebar hidden" id="agentSidebar"\>

\<!-- Taskade iFrame Embed Code --\>

\<iframe allow="clipboard-read; clipboard-write"

src="[https://www.taskade.com/a/01JJYWJXPXH1694Y9G6RJZGBP9](https://www.taskade.com/a/01JJYWJXPXH1694Y9G6RJZGBP9)"

width="600"

height="400"

frameborder="0"

allowfullscreen\>

\</iframe\>

\</aside\>

\</div\>

\<!-- Loading Indicator --\>

\<div id="loading-indicator" class="hidden"\>Processing...\</div\>

\<!-- Footer --\>

\<footer\>

\<p\>&copy; 2023 DarkNote App\</p\>

\</footer\>

\<script\>

// IIFE to avoid polluting the global scope

(() =\> {

'use strict';

// --------------------- //

// DOM Elements

// --------------------- //

const noteInput = document.getElementById('noteInput');

const titleInput = document.getElementById('titleInput');

const tagInput = document.getElementById('tagInput');

const saveButton = document.getElementById('saveButton');

const clearButton = document.getElementById('clearButton');

const deleteButton = document.getElementById('deleteButton');

const savedNotesList = document.getElementById('savedNotesList');

const searchInput = document.getElementById('searchInput');

const preview = document.getElementById('preview');

const togglePreviewButton = document.getElementById('togglePreviewButton');

const toggleGPTPreviewButton = document.getElementById('toggleGPTPreviewButton');

const exportButton = document.getElementById('exportButton');

const charCount = document.getElementById('charCount');

const aiActionSelect = document.getElementById('aiActionSelect');

const performAIActionButton = document.getElementById('performAIActionButton');

const customPromptInput = document.getElementById('customPromptInput');

const summary = document.getElementById('summary');

const gptPreviewSection = document.getElementById('gptPreview');

const gptResponseDiv = document.getElementById('gptResponse');

const loadingIndicator = document.getElementById('loading-indicator');

const editorPreview = document.querySelector('.editor-preview');

const toggleAgentSidebarButton = document.getElementById('toggleAgentSidebarButton');

const agentSidebar = document.getElementById('agentSidebar');

// --------------------- //

// Global Variables

// --------------------- //

let notes = [];

let currentNoteIndex = -1;

let autoSaveTimer;

const AUTO\_SAVE\_INTERVAL = 120000; // 2 minutes

// --------------------- //

// Event Listeners

// --------------------- //

document.addEventListener('DOMContentLoaded', () =\> {

loadNotes();

updateCharCount();

updatePreview();

});

saveButton.addEventListener('click', saveNote);

clearButton.addEventListener('click', clearInputs);

deleteButton.addEventListener('click', deleteNote);

searchInput.addEventListener('input', (e) =\> renderSavedNotes([e.target](http://e.target).value));

noteInput.addEventListener('input', () =\> {

updateCharCount();

updatePreview();

startAutoSave();

});

titleInput.addEventListener('input', startAutoSave);

tagInput.addEventListener('input', startAutoSave);

noteInput.addEventListener('keydown', handleKeyboardShortcuts);

togglePreviewButton.addEventListener('click', togglePreview);

toggleGPTPreviewButton.addEventListener('click', toggleGPTPreview);

exportButton.addEventListener('click', exportNotes);

aiActionSelect.addEventListener('change', updateAIButtonText);

performAIActionButton.addEventListener('click', handleAIAction);

// Keyboard Shortcut for MD Preview (Alt+V)

document.addEventListener('keydown', function (event) {

if (event.altKey && event.key === 'v') {

event.preventDefault();

togglePreview();

}

});

// Keyboard Shortcut for GPT Preview (Alt+G)

document.addEventListener('keydown', function(event) {

if (event.altKey && event.key.toLowerCase() === 'g') {

event.preventDefault();

toggleGPTPreview();

}

});

// New Event Listener for Toggling Taskade AI Agent Sidebar (Alt+A)

toggleAgentSidebarButton.addEventListener('click', toggleAgentSidebar);

document.addEventListener('keydown', function(event) {

if (event.altKey && event.key.toLowerCase() === 'a') {

event.preventDefault();

toggleAgentSidebar();

}

});

// --------------------- //

// Functions

// --------------------- //

function saveNote() {

const title = titleInput.value.trim();

const content = noteInput.value.trim();

const tags = tagInput.value.split(',').map(tag =\> tag.trim()).filter(tag =\> tag !== '');

if (!title && !content) {

alert('Please enter a title or content to save the note.');

return;

}

const noteData = {

title: title || 'Untitled',

content: content,

tags: tags,

timestamp: new Date().toISOString()

};

if (currentNoteIndex \> -1) {

notes[currentNoteIndex] = noteData;

} else {

notes.unshift(noteData);

}

localStorage.setItem('notes', JSON.stringify(notes));

clearInputs();

renderSavedNotes();

currentNoteIndex = -1;

}

function loadNotes() {

const storedNotes = localStorage.getItem('notes');

notes = storedNotes ? JSON.parse(storedNotes) : [];

renderSavedNotes();

}

function deleteNote() {

if (currentNoteIndex \> -1) {

if (confirm('Are you sure you want to delete this note?')) {

notes.splice(currentNoteIndex, 1);

localStorage.setItem('notes', JSON.stringify(notes));

clearInputs();

renderSavedNotes();

currentNoteIndex = -1;

}

} else {

alert('No note selected to delete.');

}

}

function clearInputs() {

titleInput.value = '';

tagInput.value = '';

noteInput.value = '';

customPromptInput.value = '';

aiActionSelect.selectedIndex = 0;

charCount.textContent = '0 characters, 0 words';

preview.innerHTML = '';

summary.innerText = '';

summary.classList.remove('visible');

gptResponseDiv.innerText = '';

gptPreviewSection.classList.add('hidden');

toggleGPTPreviewButton.textContent = 'GPT Preview';

clearTimeout(autoSaveTimer);

currentNoteIndex = -1;

}

function renderSavedNotes(searchTerm = '') {

savedNotesList.innerHTML = '';

const categories = {};

notes.forEach((note, index) =\> {

const noteTitle = note.title || 'Untitled';

const noteContent = note.content || '';

const noteTags = note.tags || [];

if (

noteTitle.toLowerCase().includes(searchTerm.toLowerCase()) ||

noteContent.toLowerCase().includes(searchTerm.toLowerCase()) ||

noteTags.some(tag =\> tag.toLowerCase().includes(searchTerm.toLowerCase()))

) {

const category = noteTags[0] || 'Uncategorized';

if (!categories[category]) {

categories[category] = [];

}

categories[category].push({ title: noteTitle, index });

}

});

const sortedCategories = Object.keys(categories).sort((a, b) =\>

a.toLowerCase().localeCompare(b.toLowerCase())

);

sortedCategories.forEach(category =\> {

const categoryDiv = document.createElement('div');

categoryDiv.classList.add('category');

const categoryHeader = document.createElement('div');

categoryHeader.classList.add('category-header');

categoryHeader.textContent = category;

[categoryHeader.style](http://categoryHeader.style).cursor = searchTerm.trim() === '' ? 'pointer' : 'default';

const categoryNotes = document.createElement('div');

categoryNotes.classList.add('category-notes');

[categoryNotes.style](http://categoryNotes.style).display = searchTerm.trim() === '' ? 'none' : 'block';

categories[category].forEach(note =\> {

const noteElement = document.createElement('div');

noteElement.classList.add('saved-note');

noteElement.textContent = note.title;

noteElement.addEventListener('click', () =\> {

clearTimeout(autoSaveTimer);

currentNoteIndex = note.index;

const loadedNote = notes[note.index];

titleInput.value = loadedNote.title || '';

tagInput.value = (loadedNote.tags || []).join(', ');

noteInput.value = loadedNote.content || '';

updateCharCount();

updatePreview();

});

categoryNotes.appendChild(noteElement);

});

categoryDiv.appendChild(categoryHeader);

categoryDiv.appendChild(categoryNotes);

savedNotesList.appendChild(categoryDiv);

});

if (searchTerm.trim() === '') {

const allCategoryNotes = document.querySelectorAll('.category-notes');

allCategoryNotes.forEach(catNotes =\> [catNotes.style](http://catNotes.style).display = 'none');

}

}

function updateCharCount() {

const content = noteInput.value;

const chars = content.length;

const words = content.trim() === '' ? 0 : content.trim().split(/\s+/).length;

charCount.textContent = `${chars} character${chars !== 1 ? 's' : ''}, ${words} word${words !== 1 ? 's' : ''}`;

}

function startAutoSave() {

clearTimeout(autoSaveTimer);

autoSaveTimer = setTimeout(() =\> {

saveNote();

console.log('Auto-saved');

}, AUTO\_SAVE\_INTERVAL);

}

function updatePreview() {

let content = noteInput.value;

let formattedContent = content

.replace(/^#{1,6}\s+(.+)/gm, (match, p1) =\> {

const level = match.trim().split(' ')[0].length;

return `<h${level}>${p1}</h${level}>`;

})

.replace(/\*\*(.+?)\*\*/g, '\<strong\>$1\</strong\>')

.replace(/\*(.+?)\*/g, '\<em\>$1\</em\>')

.replace(/`(.+?)`/g, '\<code\>$1\</code\>')

.replace(/^---$/gm, '\<hr\>')

.replace(/\n\n+/g, '\<br\>\<br\>')

.replace(/\\n/g, '\<br\>')

.replace(/\[\[([^\]]+)\]\]/g, (match, noteTitle) =\> {

return `<a href="#" class="backlink" data-title="${noteTitle}">${noteTitle}</a>`;

});

preview.innerHTML = formattedContent;

const backlinks = preview.querySelectorAll('.backlink');

backlinks.forEach(link =\> {

link.addEventListener('click', (e) =\> {

e.preventDefault();

const noteTitle = [e.target](http://e.target).getAttribute('data-title');

openNoteByTitle(noteTitle);

});

});

}

function openNoteByTitle(title) {

const noteIndex = notes.findIndex(note =\> note.title === title);

if (noteIndex !== -1) {

clearTimeout(autoSaveTimer);

currentNoteIndex = noteIndex;

const loadedNote = notes[noteIndex];

titleInput.value = loadedNote.title || '';

tagInput.value = (loadedNote.tags || []).join(', ');

noteInput.value = loadedNote.content || '';

updateCharCount();

updatePreview();

} else {

alert(`Note titled "${title}" not found.`);

}

}

function togglePreview() {

editorPreview.classList.toggle('preview-visible');

if (editorPreview.classList.contains('preview-visible')) {

togglePreviewButton.textContent = 'Hide Preview';

} else {

togglePreviewButton.textContent = 'MD Preview';

summary.classList.remove('visible');

gptPreviewSection.classList.add('hidden');

toggleGPTPreviewButton.textContent = 'GPT Preview';

}

}

function toggleGPTPreview() {

gptPreviewSection.classList.toggle('hidden');

toggleGPTPreviewButton.textContent = gptPreviewSection.classList.contains('hidden') ? 'GPT Preview' : 'Hide GPT Preview';

}

function exportNotes() {

const exportContent = notes

.map(note =\>

`Title: ${note.title || 'Untitled'}\nTags: ${note.tags.join(', ')}\n\n${note.content}\n\n---\n\n`

)

.join('');

const blob = new Blob([exportContent], { type: 'text/plain' });

const url = URL.createObjectURL(blob);

const a = document.createElement('a');

a.href = url;

[a.download](http://a.download) = 'exported\_notes.txt';

[a.click](http://a.click)();

URL.revokeObjectURL(url);

}

function handleKeyboardShortcuts(e) {

if (e.ctrlKey || e.metaKey) {

switch (e.key.toLowerCase()) {

case 'b':

e.preventDefault();

insertText('\*\*', '\*\*', 'bold text');

break;

case 'i':

e.preventDefault();

insertText('\*', '\*', 'italic text');

break;

}

}

}

function insertText(before, after, defaultText) {

const start = noteInput.selectionStart;

const end = noteInput.selectionEnd;

const selectedText = noteInput.value.substring(start, end);

const replacement = before + (selectedText || defaultText) + after;

noteInput.value = noteInput.value.substring(0, start) + replacement + noteInput.value.substring(end);

noteInput.focus();

noteInput.setSelectionRange(start + before.length, start + replacement.length - after.length);

updatePreview();

}

function updateAIButtonText() {

const selectedAction = aiActionSelect.options[aiActionSelect.selectedIndex].text;

performAIActionButton.textContent = `Perform ${selectedAction}`;

}

async function handleAIAction() {

const noteContent = noteInput.value.trim();

const selectedAction = aiActionSelect.value;

const customPrompt = customPromptInput.value.trim();

if (!noteContent) {

alert('Please enter some text in the note.');

return;

}

performAIActionButton.disabled = true;

performAIActionButton.textContent = 'Processing...';

loadingIndicator.classList.remove('hidden');

try {

let prompt;

switch (selectedAction) {

case 'summarize':

prompt = `${customPrompt || 'Please summarize the following text:'}\n\n${noteContent}`;

break;

case 'generateIdeas':

prompt = `${customPrompt || 'Please generate novel ideas based on the following text:'}\n\n${noteContent}`;

break;

case 'extractWisdom':

prompt = `${customPrompt || 'Please extract the key wisdom or insights from the following text:'}\n\n${noteContent}`;

break;

default:

prompt = `${customPrompt}\n\n${noteContent}`;

}

const aiResponse = await getChatGPTResponse(prompt);

gptResponseDiv.innerText = aiResponse;

if (gptPreviewSection.classList.contains('hidden')) {

toggleGPTPreview();

}

} catch (error) {

console.error('Error:', error);

alert('An error occurred while processing the AI action.');

} finally {

performAIActionButton.disabled = false;

performAIActionButton.textContent = 'GPT';

loadingIndicator.classList.add('hidden');

}

}

async function getChatGPTResponse(prompt) {

const apiKey = 'YOUR\_OPENAI\_API\_KEY'; // Replace with your actual API key

const endpoint = '[https://api.openai.com/v1/chat/completions](https://api.openai.com/v1/chat/completions)';

const headers = {

'Content-Type': 'application/json',

'Authorization': `Bearer ${apiKey}`,

};

const body = {

model: 'gpt-3.5-turbo',

messages: [

{ role: 'system', content: 'You are a helpful assistant.' },

{ role: 'user', content: prompt },

],

max\_tokens: 500,

temperature: 0.7,

};

try {

const response = await fetch(endpoint, {

method: 'POST',

headers: headers,

body: JSON.stringify(body),

});

if (!response.ok) {

const errorData = await response.json();

throw new Error(errorData.error.message || 'An error occurred while communicating with the OpenAI API.');

}

const data = await response.json();

return data.choices[0].message.content.trim();

} catch (error) {

console.error('Error fetching ChatGPT response:', error);

throw error;

}

}

function toggleAgentSidebar() {

agentSidebar.classList.toggle('hidden');

}

// New Keyboard Shortcut for toggling Agent Sidebar (Alt+A)

document.addEventListener('keydown', function(event) {

if (event.altKey && event.key.toLowerCase() === 'a') {

event.preventDefault();

toggleAgentSidebar();

}

});

})();

\</script\>

\</body\>

\</html\>

