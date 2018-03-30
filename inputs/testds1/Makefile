all: sub-1_T1w_5mm.nii.gz sub-1_T1w_5mm_rot1.nii.gz

%_5mm.nii.gz: %.nii.gz
	3dresample -prefix $@ -input $< -dxyz 5 5 5

%_rot1.nii.gz: %.nii.gz
	3drotate -prefix $@ -bshift 10S 0 0 -rotate 30R 0 0 $<
