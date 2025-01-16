
import tkinter as tk
from tkinter import filedialog, messagebox
import os
from reportlab.pdfgen import canvas
from reportlab.lib.pagesizes import letter
from reportlab.lib.styles import ParagraphStyle
from reportlab.lib.enums import TA_LEFT, TA_CENTER
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer
from reportlab.lib.units import inch

class MaliciousPDFGeneratorApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Malicious PDF Generator")

        # Create GUI elements
        self.input_frame = tk.Frame(self.root)
        self.input_frame.pack()

        self.payload_label = tk.Label(self.input_frame, text="Payload:")
        self.payload_label.pack()

        self.payload_entry = tk.Entry(self.input_frame, width=50)
        self.payload_entry.pack()

        self.template_label = tk.Label(self.input_frame, text="Template:")
        self.template_label.pack()

        self.template_entry = tk.Entry(self.input_frame, width=50)
        self.template_entry.pack()

        self.output_label = tk.Label(self.input_frame, text="Output:")
        self.output_label.pack()

        self.output_entry = tk.Entry(self.input_frame, width=50)
        self.output_entry.pack()

        self.generate_button = tk.Button(self.input_frame, text="Generate", command=self.generate_pdf)
        self.generate_button.pack()

        self.status_label = tk.Label(self.input_frame, text="")
        self.status_label.pack()

        self.browse_button = tk.Button(self.input_frame, text="Browse", command=self.browse_output)
        self.browse_button.pack()

        self.clear_button = tk.Button(self.input_frame, text="Clear", command=self.clear_fields)
        self.clear_button.pack()

    def generate_pdf(self):
        payload = self.payload_entry.get()
        template = self.template_entry.get()
        output = self.output_entry.get()

        if not payload or not template or not output:
            self.status_label.config(text="Please fill in all fields")
            return

        try:
            self.create_pdf(payload, template, output)
            self.status_label.config(text="PDF generated successfully")
        except Exception as e:
            self.status_label.config(text="Error generating PDF: " + str(e))

    def create_pdf(self, payload, template, output):
        pdf = SimpleDocTemplate(output, pagesize=letter)
        styles = {
            'Title': ParagraphStyle(
                name='Title',
                fontSize=24,
                leading=26,
                alignment=TA_CENTER,
                textColor=(0.2, 0.2, 0.2),
                backgroundColor=(0.9, 0.9, 0.9),
                fontName='Helvetica-Bold',
            ),
            'BodyText': ParagraphStyle(
                name='BodyText',
                fontSize=12,
                leading=14,
                alignment=TA_LEFT,
                textColor=(0.2, 0.2, 0.2),
                backgroundColor=(0.9, 0.9, 0.9),
                fontName='Helvetica',
            ),
        }

        story = []
        story.append(Paragraph(payload, styles['Title']))
        story.append(Spacer(1, 12))
        story.append(Paragraph(template, styles['BodyText']))

        pdf.build(story)

    def browse_output(self):
        output = filedialog.asksaveasfilename(defaultextension=".pdf", filetypes=[("PDF files", "*.pdf")])
        self.output_entry.delete(0, tk.END)
        self.output_entry.insert(0, output)

    def clear_fields(self):
        self.payload_entry.delete(0, tk.END)
        self.template_entry.delete(0, tk.END)
        self.output_entry.delete(0, tk.END)
        self.status_label.config(text="")

if __name__ == "__main__":
    root = tk.Tk()
    app = MaliciousPDFGeneratorApp(root)
    root.mainloop()
