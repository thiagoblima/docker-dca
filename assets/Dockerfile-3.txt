FROM example/nanoer
ADD notes.txt /notes.txt
CMD ["nano", "/notes.txt"]
