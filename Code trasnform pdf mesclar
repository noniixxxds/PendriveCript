import os
import tkinter as tk
from tkinter import filedialog, messagebox
from PIL import Image
import PyPDF2  # Import PyPDF2 module for PDF manipulation

def convert_to_pdf(image_paths, output_folder):
    pdf_paths = []
    for index, image_path in enumerate(image_paths, start=1):
        pdf_path = os.path.join(output_folder, f"{index:08d}.pdf")
        try:
            # Open image with PIL
            img = Image.open(image_path)
            # Convert image to PDF
            img.save(pdf_path, "PDF", resolution=100.0)
            pdf_paths.append(pdf_path)
        except Exception as e:
            print(f"Error converting {image_path} to PDF: {str(e)}")
    return pdf_paths

def merge_pdfs(paths, output_folder, output_filename):
    merger = PyPDF2.PdfMerger()
    for path in paths:
        merger.append(path)
    output_path = os.path.join(output_folder, f"{output_filename}.pdf")
    merger.write(output_path)
    merger.close()
    return output_path

def merge_pdfs_gui():
    image_paths = filedialog.askopenfilenames(title="Select JPEG image files", filetypes=[("JPEG Images", "*.jpeg")])
    if image_paths:
        output_folder = filedialog.askdirectory(title="Select the folder to save the merged PDF file")
        if output_folder:
            pdf_paths = convert_to_pdf(image_paths, output_folder)
            if pdf_paths:
                output_filename = "merged"  # Name for the merged file
                merged_file_path = merge_pdfs(pdf_paths, output_folder, output_filename)
                messagebox.showinfo("Success", f"The files have been merged and saved as '{output_filename}.pdf'.")
            else:
                messagebox.showinfo("Warning", "Failed to convert JPEG images to PDF.")
        else:
            messagebox.showinfo("Warning", "No folder selected. The operation was canceled.")
    else:
        messagebox.showinfo("Warning", "No JPEG images selected. The operation was canceled.")

# Main window configuration
root = tk.Tk()
root.title("Merge JPEG Images into One PDF")

# Button to initiate file merging
button_merge = tk.Button(root, text="Select Images and Merge into One PDF", command=merge_pdfs_gui)
button_merge.pack(pady=20)

# Run the main interface loop
root.mainloop()
